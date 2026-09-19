# Sequential-print geometry for the Micron (Anthead toolhead)

Adds collision-aware sequential printing ("Complete individual objects") for a Micron running
the Anthead toolhead, so PrusaSlicer uses a real model of the head instead of the generic
nozzle-cylinder approximation.

Bed 160 × 160. See [DESIGN.md](DESIGN.md) for how the envelope was derived and verified.

## Install

Both files go in `resources/data/printer_gantries/`.

| File | Action |
| --- | --- |
| `micron_anthead_gantry.stl` | copy into the directory |
| `micron_anthead_gantry.json` | **prepend** its object to the `printers` array in `geometries.json` |

PrusaSlicer walks `printers` in order and stops at the first `printer_notes_regex` that matches,
so the entry must go **first** in the array to take precedence.

## ⚠️ Required: printer profile notes

**The printer profile must contain `PRINTER_MODEL_MICRON` in Printer Settings → Notes.**

Nothing else selects this geometry. Matching is done purely against that field — profile name,
printer model and vendor are all ignored. Other text in Notes is fine; the marker just has to
appear somewhere in it.

Then enable **Print Settings → Output options → Complete individual objects**.

## Checking that it took

Look at the toolhead marker on the plater:

> If the plater is drawing your Anthead, the geometry entry matched and the fallback is
> dormant. Generic cone = you've lost the match and PrusaSlicer falls back to sequential
> printing limits; radius and height.

The marker and the collision model are resolved through the same lookup, so the picture is a
reliable tell. The fallback is silent — no warning, no log entry — so this is worth a glance
after any edit to Printer Notes.
