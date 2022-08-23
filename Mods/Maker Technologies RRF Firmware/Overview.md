Use this config as a base to develop RRF for your machine. This was made using pRINTERnOODLE's config (https://github.com/pRINTERnOODLE/RRF-klicky-probe-voron-2.4) and has integrated z calibration (https://github.com/pRINTERnOODLE/Auto-Z-calibration-for-RRF-3.3-or-later-and-Klicky-Probe). The board used for this config was the BTT Octopus pro 429, TMC 2209s and a Paneldue i7.

I used the AC heated bed mod, which is why the bed heater pin looks a bit weird. Do note that this pin is on by default which will start heating your bed if the pin is not defined. This will work fine for the DC bed as well, just move the bed mosfet to the 24v rail.

Pay attention to the order of the motors in config.g! I skipped over port 04.

I have also defined macros for start and end gcode, which can be called up using M98 P"/macros/start.g" 98 P"/macros/end.g"

My Micron (V2.4085), was built in between models, so there are a few things that are probabably different for you. It is a good idea to go thru bith the config and macros to make sure everything macthes up.

I am still developing a few things for this... feel free to reach out via discord for comments and contributions.

-Dom Dell Computer#0675
