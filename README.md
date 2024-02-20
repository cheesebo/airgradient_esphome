# airgradient_esphome
These are my extensions to MallocArray's AirGradient ESPhome integration repo:
  https://github.com/MallocArray/airgradient_esphome

A few files I've created to modify the LED display to cover four sensor readings rather than one, plus a few minor tweeks. 

## LED Changes

I've used the first three LEDs for CO2, with the next one off.
The next three for AQI, with the next one off.
The next one for VOC, one more is off and the last is for NOX.

|LED:    | 0 1 2 | 3 | 4 5 6 | 7 | 8 | 9 | 10 |
|-|-|-|-|-|-|-|-|
|Reading: |CO2|-|AQI|-|VOC|-|NOX|

Each has a colour grade:
|Reading| Grade based on|
|--|--|
| CO2 | Wikipedia Computing the AQI (using the same details from the MallocArray repo with some changes for the individual LED management) |
| AQI | Wikipedia AQI levels (using values calculated by *sensor_pms5003.yaml* from MallocArray repo) |
| VOC | roughly based on Sensirion SGP41 datasheet |
| NOX | roughly based on Sensirion SGP41 datasheet |
         
The ranges controlling the colours are arbitary and can be easily changed by editing the approrpiate led sensor yaml file in the packages folder

## Minor Tweeks
The *display_sh_1106_multi_page.yaml* file has been udated to show AQI rather than ug/m3 for PM2.5, and the *sensor_pms5003.yaml* file was missing an **update interval** resulting in no updates being registered.

The *ag-one.yaml* has been modified to use the local display, sensor and led yaml files, which should be in your local packages folder (if using ESPHome on Home Assistant instance this is probably the */root/config/esphome/packages* folder).

The led_***sensor***.yaml files are all pretty similar and it should be easy to change the ranges for the colour changes and the colours themselves.

## NOTE
 Using the **light.turn_on**: led_strip action will reset the colours of the LED strip - so it has been removed from the local *led_co2.yaml*. The **color_brightness** action is used instead, but, if the **light.turn_on** action is used to set the brightness, it will set the maximum brightness that **color_brightness** can reach.

**led_brightness** can be used to reset the overall brightness, but it will override the other led settings. It can be used as a one-off between installs if the strip needs its brightness resetting.

If you wish to see all the colours I've used on the strip in one static band, you can use the *led_colours_list.yaml* without the led files.
