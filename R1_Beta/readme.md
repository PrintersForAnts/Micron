## Micron R1 Beta 
![Rendering of a Micron build](https://github.com/PrintersForAnts/Micron/assets/12398294/9f905930-95b1-47f4-a604-515db16e991e)

<p align="center">
<img alt="Discord" src="https://img.shields.io/discord/825469421346226226?style=for-the-badge&logo=discord&logoColor=%2344d62c&label=Discord&labelColor=%2363666a&color=%2344d62c&link=https%3A%2F%2Fdiscord.gg%2Fdoomcube">
</p>

<p align="center">
Be sure to check out the Micron R1 beta thread on the Doomcube discord for more information 
</p>

## Change log ##

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
  * New beta rev2 Z drives that support 150mm or 152mm belt loops
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
  * New Z drives that use 150mm belt loops with proper belt tensioning 
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
GT2-150mm closed loop belt | 4 | New Z drives use 150mm belt loops instead of the 188mm 
screws | IDK | i havent gone through and checked the changes for the hardware as of yet 
MGN9H | 1 | X rail is now going to be spec as an MGN9H rail instead of MGN9C to support boop natively 
Klicky_PCB | 1 | now offical support optional as standard klikcy is still supported 
BIQU_microprobe | 1 | also now an official supported mount for those that want to use it 








