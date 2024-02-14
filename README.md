# airgradient_esphome
Extensions to MallocArray's AirGradient ESPhome integration repo 
  https://github.com/MallocArray/airgradient_esphome

These are a few files I've created to modify the LED display to cover four sensor readings:

Of the eleven LEDs:
  xxx-xxx-x-x
  CO2
      AQI
          VOC
            NOX

Each with a grade based on:
 CO2 - based on Wikipedia Computing the AQI (using the same details from the MallocArray repo with some changes for the individual LED management)
 AQI - based on Wikipedia AQI levels (using values calculated by sensor_pms5003_extended_life.yaml from MallocArray repo)
 VOC - based on Sensirion SGP41 datasheet
 NOX - based on Sensirion SGP41 datasheet
         
The ranges controlling the colours are arbitary and can be easily changed by editing the approrpiate led sensor yaml file in the packages folder

The display_sh_1106_multi_page.yaml file has been udated to show AQI rather than ug/m3 for PM2.5

The ag-one.yaml has been modified to use the local led yaml files and the display_sh_1106_multi_page yaml file - the led and display yaml files should be in your local packages folder (if using ESPHome on Home Assistant instance this is probably /root/config/esphom folder).

The led_<sensor>.yaml files are all pretty similar and it should be easy to change the ranges for the colour changes and the colours themselves.

NOTE: Using the light.turn_on: led_strip action will reset the colours of the LED strip - so it has been removed from the led_co2.yaml. The color_brightness action is used instead, but, if the light.turn_on action is used to set the brightness, it will set the maximum brightness that color_brightness can reach.

The led_colours_list.yaml will set the range of colours I've used if it is used instead of the other four led yaml files.

led_brightness can be used to reset the overall brightness, but it will override the other led settings. It can be used as a one-off between installs if the strip needs its brightness resetting.
