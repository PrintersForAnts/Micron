## Micron R1 Beta 
![Rendering of a Micron build](https://github.com/PrintersForAnts/Micron/assets/12398294/6084ce95-06f8-4391-bb22-0c11cae98a66)

[![](https://img.shields.io/discord/825469421346226226?color=teal&label=Micron&logo=discord&logoColor=fafafa)](https://discord.gg/doomcube)
Be sure to check out the Micron R1 beta thread on the Doomcube discord for more information 

## Change log ##

### 4-3-24
 Z axis
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








