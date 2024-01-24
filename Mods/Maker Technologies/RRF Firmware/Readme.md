**NO LONGER MAINTAINED**
Though this firmware will be a good place to start with, there may be config changes in RRF that may require modification to the config. I have sold my Micron so I will not be working on this anymore.

Use this config as a base to develop RRF for your machine. This was made using pRINTERnOODLE's config (https://github.com/pRINTERnOODLE/RRF-klicky-probe-voron-2.4) and has integrated z calibration (https://github.com/pRINTERnOODLE/Auto-Z-calibration-for-RRF-3.3-or-later-and-Klicky-Probe). Big thank you to them for doing most of the legwork. I did make some siginificant changes, mostly in the name of simplification and consolidation. There are still some unused macros that I will get around to cleaning up eventually, but in the meantime they have just been commented out. The hardware used for this config was the BTT Octopus pro 429, TMC 2209s, BTT wifi card and a Paneldue i7.

I used the AC heated bed mod, which is why the bed heater pin looks a bit weird. It uses a 5V relay and I used the PS_ON pin to control the bed instead of allocating a fan port. Do note that this pin is on by default which will start heating your bed if the pin is not defined. This config will work fine for the DC bed as well, just move the bed mosfet pin to the 24v rail.

Pay attention to the order of the motors in config.g! I skipped over port 04. This was because I could not get the original config to work with the correct z motor numbering. If you can figure this out please let me know! Until then, config.g tells you how to wire the z motors.

I have also defined macros for start and end gcode, which can be called up using M98 P"/macros/start.g" and M98 P"/macros/end.g" respectivly. 

My Micron (V2.4085), was built in between models, so there are a few things that are probabably different for you. It is a good idea to go through both the config and macros to make sure everything macthes up.

More information on how to get RRF on your board (and compatible boards themselves) can be found here: https://teamgloomy.github.io/

I have been using this config for quite a while with great success. I do plan on still implimenting a few things in the distant future. Specfically accelerometer support. RRF can be quite an uphill battle with these things though, so please be patient. 

-DomDellComputer
