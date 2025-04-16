## Micron R1 Beta 
![Rendering of a Micron build](https://github.com/user-attachments/assets/76d17d27-6f04-4e86-9524-b83c739ac207)
<p align="center">
<img alt="Discord" src="https://img.shields.io/discord/825469421346226226?style=for-the-badge&logo=discord&logoColor=%2344d62c&label=Discord&labelColor=%2363666a&color=%2344d62c&link=https%3A%2F%2Fdiscord.gg%2Fdoomcube">
</p>

<p align="center">
Be sure to check out the Micron R1 beta thread on the Doomcube discord for more information 
</p>


## Change log ##

### 01-20-2025
* fixed issues #143 , #141, #138 , #137
* Updated CAD to RC1 status
* uploaded WIP manual with updated preloaded nut callouts 

### 10-17-2024
* Added G2Z Cad and organized all the STLS (Z drives and skirts) G2Z uses same foot mounts from R1Z and skirt accent pieces 
* fixed Pinned XY joints hole sizes to now all be 3.2mm 
* Updated latest assembly to include [Anthead](https://github.com/PrintersForAnts/AntHead)

### 9-20-2024
* increased tension travel on the front idlers by 5mm (from 3mm to 8mm) , minor changes to the front cover of the idler as well

### 9-18-2024
* fixed incorrect counterbore bridging on the rear bowden entry files (thanks to user named Yell for finding that)

### 9-12-2024
* added CNC gantry top bearing mount
* Updated all the umbilical mounts to accomodate the new top bearing mount, as it was interfearing
* removed the YC8 version of the umbilical
* updated cad assembly to v59 


### 9-10-2024
* Added new top bearing support for a double shear bearing on the AB motors 

### 9-5-2024
* cleaned up main cad assembly 
* posted link to fusion source assembly file to be downloaded
* adjusted gantry files to no longer need built in printed shim, now there are shims on both sides of every bearing stack 

### 9-3-2024
* added missing filter files 
* fixed naming issues on certain files 

### 9-2-2024
* added new under bed carbon filter
* started on CAD assembly clean up 
* renamed various files 

### 8-22-2024 
* cleaned up files

### 8-11-2024
* updated the Hula foot mounts to the latest version that works with the bottom panel
* added new TFT35 display front skirt 
* updated latest cad assembly v55
* removed old cad files no longer needed (moved hula cad files into main assembly)

### 8-2-2024
* organized panel clip files
* updated latest cad assembly v54
* added dual color rear bowden entry option

### 8-1-2024
* Updated Z drives for better printability to match new skirt accent pieces
* Added under bed filter from KyleGB to the main repo (still need STLs)

### 7-27-2024
* fixed waveshare accent pieces
* updated latest cad assembly v52
* updated skirts with new accent pieces as well as bottom panel mounting provisions
  

### 7-25-2024
* Updated z belt cover accent cover to fit better
* added twist lock panel clips for 3mm foam and panels
* fixed printing orientation for rail stops and umbilical mounts

### 7-23-2024
* Updated R1 Skirts to now include accent strips along the bottom as well as allow for a bottom panel to fit
* Updated skirts to they are all the same height , some had about ~1mm difference between them 
* Updated the waveshare mount to now us m2 self tapping screws instead of filament to keep bezel on 
* Updated Z drive foot mount to accommodate  bottom panel 

### 7-23-2024
* Update Beacon mount to work with older Rev D beacon probes 
* Added a new rear bowden entry set, supporting m10 collet, ECAS collet, or No collet 
* Added R1 style stock panel clips (tool less panel clips are coming soon as an option as well)
* Added fixed Z belt covers to better fit with the R1 Z belt location
* Organized the panel file directory 

### 7-15-2024
* Added Beacon probe mount

### 7-08-24
* Added 120x120 build R1 Cad assembly
* Added rear skirts for 120x120 builds 
* Organized files into 120 and 180 specific folders 

### 7-05-24
* added rear power inlet skirts
* updated printed rail stops to match the style of R1 update (low poly look)
* added keystone blank model to fill the keystone slots on the rear skirt if not used 

### 7-02-24
* updated Z drive tensioner body to use longer m3x25 instead of m3x20
* added optional Hula feet adapters for R1 and G2Z
* updated latest cad assembly

### 6-18-24
* uploaded side skirts and 4.3 waveshare display front skirt

### 6-2-24
* changed hex pattern on Z drives to make them easier to print 

### 5-21-24
* adjust the location of the Z gantry belts pulley to fit in the front idlers better ([#124](https://github.com/PrintersForAnts/Micron/issues/124))

### 5-14-24
* fixed z drive issue with inconsistencies with both A and B z drives ([#120](https://github.com/PrintersForAnts/Micron/issues/120))
* updated z tensioner bearing overhang to be easier to print ([#122](https://github.com/PrintersForAnts/Micron/issues/122))

### 5-7-24
* Added ziptie spot on to klicky dock

### 5-6-24
 * Updated Z drives to fit powge and formbot metal 64T pulleys ([#115](https://github.com/PrintersForAnts/Micron/issues/115))
 * Updated Z idlers to fit toothed pulleys with a flange of 13mm OD ([#116](https://github.com/PrintersForAnts/Micron/issues/116))
 * raised klicky dock , it was hanging too low ([#117](https://github.com/PrintersForAnts/Micron/issues/117))
 * updated spool holder to now work with 3mm foam ([#118](https://github.com/PrintersForAnts/Micron/issues/118))

### 4-6-24
 * added pushed rigid z joints
 * new z belt covers
 * new bowden tube holder
 * new removable spool holder (modified from LDOs)

### 4-5-24
  *  Added Nema14 Z motor mounts

### 4-3-24
  * New beta rev2 Z drives with the 152mm belt loops
  * Shrunk entire body by 5mm or so
  * rotated the Z drives 180deg, this makes it easier to retention the closed loop belts after they are assembled if needed (thanks [@Squirrel-brain](https://github.com/Squirrel-brain)) 


### Initial Beta Release
Gantry 
  * Swapped rear extrusion and Z chain around
  * Fixed all belt path issues with the gantry
  * Gave every piece a low poly / stealthy look to them
  * New z joints that are stronger/ less prone to cracking
  * Added support for 3mm pins OR screws for the gantry
  * Removed support for the printed Z chain (will revisit later)
  * Implemented the BFI idlers for the AB belts
  * Modified the BFI idlers from clees repo to fix the belt path for the R1 gantry 
    
Z axis
  * New Z drives that use 152mm belt loops with proper belt tensioning 
  * Implemented the BZI idlers for the Z belts
  * Modified BZI to support both toothed idlers and bearing stacks (there are different parts named accordingly)
    

Panels/Door/Skirts
  * New door hinge/ latch system that no longer needs the magnet latch on the inside of the printer
  * Door now needs 3mm foam to help seal the enclosure better
  * Panel clips will be coming later as will skirts




## BOM Changes (Subject to change)
Item  |Qty | Notes
 ----|----|----|
GT2-16-Toothed Idler | 6 | XY-Joints and Z idlers now use toothed idlers by default, bearing stacks will still work 
GT2-152mm closed loop belt | 4 | New Z drives use 152mm belt loops instead of the 188mm 
screws | IDK | i havent gone through and checked the changes for the hardware as of yet 
MGN9H | 1 | X rail is now going to be spec as an MGN9H rail instead of MGN9C to support boop natively 
Klicky_PCB | 1 | now offical support optional as standard klikcy is still supported 
BIQU_microprobe | 1 | also now an official supported mount for those that want to use it 








