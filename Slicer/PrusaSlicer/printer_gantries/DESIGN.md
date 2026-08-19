# Design notes — Micron / Anthead sequential-print geometry

> **Derived with [Claude](https://claude.com/claude-code).** The slice semantics were read out
> of the PrusaSlicer source, the envelope was measured from the toolhead mesh, and both
> verification passes below were run programmatically. Reviewed by a human before submission,
> but treat the numbers as machine-derived and check them against your own hardware.

How the envelope in `micron_anthead_gantry.json` was derived from the toolhead mesh, and why it
is shaped the way it is. Installation is covered in [README.md](README.md).

## How PrusaSlicer consumes the file

`ArrangeHelper.cpp :: get_printer_geometry()` matches `printer_notes_regex` against the printer
profile's Notes, parses the slice list, and hands it to `libseqarrange`. For every height *h* in
the file it takes the convex hull of everything in the object **above** *h*:

```cpp
Polygon pgn = its_convex_hull_2d_above(raw_mesh.its, matrix, height - offset.z());
```

and pairs it with that slice's polygons. Consequences worth knowing:

- Each slice is an independent constraint — "no object material above *h* may fall inside these
  polygons" — so a polygon at height *h* behaves like an **infinite column from h upward**. It
  only *needs* to enclose the toolhead between *h* and the next height, but may be larger.
- Heights are measured from the bed, which coincides with "above the nozzle" in the worst case
  (nozzle down on layer 1). That is why the STL is authored with the nozzle tip at z = 0.
- Coverage only has to hold in aggregate. The `h = 33` entry contains *only* the rail; the body
  of the head above 33 mm is already handled by the `h = 3` box, because the hull above 3 mm is
  a superset of the hull above 33 mm.

### `convex` vs `box`

`convex` is a true Minkowski sum of the two outlines. `box` runs through
`extend_PolygonBoxUnreachableZone()`, which takes the **axis-aligned bounding box of both** and
adds the extents. That is why the rail is written as ±100 rather than its true ±125: on a
160 mm bed, an object's AABB offset by 100 mm already spans the whole plate, so any half-extent
past the plate is equivalent. It is a cheap total constraint, not a measurement.

### Why the polygons are point-reflected

The configuration-space obstacle for a rigid tool *T* against an object *O* is *O* ⊕ (−*T*).
`libseqarrange` sums the stored polygon directly, with no negation step anywhere in the
pipeline:

```cpp
// seq_preprocess.cpp — extend_PolygonConvexUnreachableZone()
ClipperLib::MinkowskiSum(extruder_polygons[i].points, polygon.points, paths, true);
```

so the file has to hold **−T** already. For a shape reflected through the origin that is a 180°
rotation about Z:

```
x_json = -x_stl     y_json = -y_stl     z_json = z_stl
```

## Re-zeroing the mesh

The source mesh is not authored on the nozzle — the tip sits at (−0.089, −12.792, −53.688),
with X = 0 on the gantry centreline and Z = 0 somewhere in the carriage. Everything here is
expressed after translating that point to the origin, which puts the model at X ±125,
Y −26.3…54.3, Z 0…129.

This matters for display as well as measurement. PrusaSlicer positions a custom gantry marker
with a pure translation:

```cpp
: Geometry::translation_transform(m_world_position.cast<double>());
```

No rotation, no offset — the flip and `m_model_z_offset` only apply to the generic fallback
cone. The model origin *is* the nozzle, so the un-re-zeroed mesh renders 53.7 mm low.

The shipped STL is that translation applied, decimated to 70 k triangles (3.5 MB, down from
51 MB ASCII). Bounds should read roughly `[[-124.9, -26.4, -0.015], [125.1, 54.3, 128.95]]`.

The X rail landing 21.4–42.9 mm behind the nozzle at 33–48 mm up confirms **+Y = rear**, the
same convention the Prusa files use, so no extra rotation is needed beyond the reflection.

## Slice-by-slice

| h | type | polygon (printer frame) | covers | measured mesh |
| --- | --- | --- | --- | --- |
| 0 | convex | X −3.4…3.3, Y −3.6…3.4 | nozzle cone — the only thing below 1 mm | X −1.75…1.5, Y −1.75…1.5 |
| 1 | convex | legs X −26.2…−4.7 and 4.8…26.3 (Y −26.8…34.2); block ±8.5 | duct shrouds, heater block and sock | legs Y −24.8…32.2, block ±6.5 |
| 3 | convex | X −29.7…29.8, Y −28.3…47.7 | full toolhead body, carries to z = 33 and under the rail to 49 | X −27.8…27.5, Y −26.5…45.5 |
| 33 | box | X ±100, Y 19.4…45.2 | MGN rail + 1515 X extrusion, spans the machine | Y 21.4…42.9, z 33…48 |
| 49 | convex | X −30.9…35.3 (Y −28.3…21.4); X −30.4…27.8 (Y 43.2…56.4) | extruder deck, motor and blower above the rail | X −28.8…33, Y −26.5…54.3 |

Notes on the individual slices:

- **The shrouds come down to 1.5 mm above the nozzle tip**, much tighter than any Prusa head.
  That is why slice 0 is only ±3.4 and slice 1 starts at 1 mm rather than the 2–3 mm Prusa
  uses. Below 1 mm the nozzle cone is genuinely the only thing there.
- **Slice 1 is three rectangles.** The duct legs leave a 9.5 mm slot at the centreline occupied
  only by the heater block. Collapsing to a single rectangle
  `-26.3,-34.2;26.3,-34.2;26.3,26.8;-26.3,26.8` costs about 9 % more forbidden area and is
  easier to hand-edit — either is correct.
- **Slice 49 is split for a reason.** The middle strip of the upper assembly falls inside slice
  33, which already blocks that Y band across the whole plate for anything taller than 33 mm.
  Splitting around it is free.
- **Being CoreXY helps.** The X extrusion translates in Y with the toolhead, so it is rigid
  relative to the nozzle and maps cleanly onto slice 33. The Y rails and frame sit outside the
  plate, and a tall model hits the underside of the gantry or the sides of the head long before
  it clears anything, so no additional constraint is needed above the head.

Envelope carries a **2 mm** margin over the measured geometry, mid-range for what Prusa ships
(their MINI file runs 1–3 mm).

## Verification

Two independent passes:

1. Every band rasterised at 0.25 mm and tested against the union of all slices at or below its
   start height.
2. 383 648 points sampled uniformly over the mesh surface, point-reflected, each tested for
   containment in the polygons applicable at its own Z.

| band | slices in force | mesh footprint mm² | uncovered mm² |
| --- | --- | --- | --- |
| z ∈ [0, 1) | 0 | 6.1 | 0.0 |
| z ∈ [1, 3) | 0, 1 | 895.7 | 0.0 |
| z ∈ [3, 33) | 0–3 | 3228.3 | 0.0 |
| z ∈ [33, 49) | 0–33 | 6273.3 | 0.0 |
| z ∈ [49, 129) | all | 4221.1 | 0.0 |

Surface sampling: 383 648 points inside ±100 mm, zero uncovered.

## Regenerating

`gen_geom.py` rebuilds the entry from a mesh:

```bash
python3 gen_geom.py Micron_Anthead_Gantry.stl \
    --bed 160x160 --margin 2 \
    --heights 0,1,3,49 --box-heights 33 \
    --regex '.*PRINTER_MODEL_MICRON.*' \
    --gantry-file micron_anthead_gantry.stl
```

It auto-detects the nozzle tip as the lowest isolated feature (override with `--nozzle X,Y,Z`),
gives each convex slice ownership of the band from its own height to the next, pulls
machine-spanning members out into `box` slices, and prints a per-band coverage audit to stderr.
If a band leaks it says so and where — add a height there or raise the margin.

Requires `trimesh numpy scipy pillow`.

## Gotcha for anyone editing the JSON by hand

**Do not put two slices at the same height.** PrusaSlicer stores them in a
`std::map<coord_t, std::vector<Polygon>>` and uses `insert()`, which does not overwrite — a
second entry at the same height is silently dropped. The shipped file already does this: the
CoreOne and CoreOne L entries each declare two slices at `h = 23`, and the second never reaches
the solver. Put multiple shapes in one slice's `polygons` array instead.

## Relationship to the Radius / Height settings

While the entry matches, `extruder_clearance_radius` and `extruder_clearance_height` are unused
for collision detection — `get_printer_geometry()` only builds the cylinder fallback when the
slice list comes back empty (Notes blank, JSON unparseable, or no regex match).

Two things still apply:

- Keep both **non-zero**. `PrintConfigDef::validate()` rejects `<= 0`.
- The radius feeds `min_object_distance()`, which sets the lower bound of the Arrange tool's
  "distance from objects" range when Complete individual objects is on. Inflating it costs
  plate density.

If you want the fallback to be honest rather than decorative: `height = 33` (nozzle tip to the
underside of the X rail) and `radius = 55` — the fallback is a *square* of half-side `r` centred
on the nozzle, and the head reaches Y +54.3 at the rear. That 55 mm then becomes the arrange
spacing floor, which is punishing on a 160 mm bed, so it is a real trade-off.

## Source references

PrusaSlicer master:

- `src/libslic3r/ArrangeHelper.cpp`
- `src/libseqarrange/src/seq_preprocess.cpp`
- `src/libseqarrange/include/libseqarrange/seq_interface.hpp`
- `src/slic3r/GUI/GCodeViewer.cpp`, `src/slic3r/GUI/GLCanvas3D.cpp`
