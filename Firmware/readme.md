# Micron Firmware Config

run this script in your terminal to download the basic Micron cfg, 

```
cd ~/printer_data/config && curl -s https://api.github.com/repos/PrintersForAnts/Micron/contents/Firmware/printer_data/config | grep download_url | cut -d '"' -f 4 | xargs -n1 curl -sOL
cd ~/printer_data/gcodes && curl -s https://api.github.com/repos/PrintersForAnts/Micron/contents/Firmware/printer_data/gcodes | grep download_url | cut -d '"' -f 4 | xargs -n1 curl -sOL
```

make sure to go through the entire cfg and uncomment the sections required 

* Build Size (120 or 180) 
* MCU
* Toolhead MCU
* Probe


This will download he default config as well as a sample gcode for printing a test cube

to initiate the test cube print, run the macro 

`PRINT_TEST_CUBE` 
then your webui will prompt you to choose which filament type you are using for the test print 
<img width="403" height="164" alt="image" src="https://github.com/user-attachments/assets/33613615-f327-4eb0-b787-492b8c354513" />


