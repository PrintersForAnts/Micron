# Micron Firmware Config

run this script in your terminal to download the basic Micron cfg, 
make sure to go through the entire cfg and setup the pin names for your controller as well as uncomment the sections required for your build size (120 or 180) 
there is also probe sections to uncomment based on the probe you are using (klicky, beacon, microprobe) 



```
cd ~/printer_data/config && curl -s https://api.github.com/repos/PrintersForAnts/Micron/contents/Firmware/printer_data/config | grep download_url | cut -d '"' -f 4 | xargs -n1 curl -sOL
cd ~/printer_data/gcodes && curl -s https://api.github.com/repos/PrintersForAnts/Micron/contents/Firmware/printer_data/gcodes | grep download_url | cut -d '"' -f 4 | xargs -n1 curl -sOL
