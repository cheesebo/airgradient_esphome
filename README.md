# airgradient_esphome
Extensions to MallocArray's AirGradient repo

Added some files to extend the LED display to cover four sensor readings:

Of the eleven LEDs:
  xxx-xxx-x-x
  CO2
      AQI
          VOC
            NOX

Each with a grade based on:
 CO2 - based on Wikipedia Computing the AQI (this is from the MallocArray repo with some changes for the LED management)
 AQI - based on Wikipedia UK AQI levels
 VOC - based on Sensirion SGP41 datasheet
 NOX - based on Sensirion SGP41 datasheet
         
The ranges are arbitary and can be easily changed by editing the approrpiate yaml file.

Place the ag-one.yaml in /root/config/esphom folder (if using ESPHome on Home Assistant instance)
Create a folder called packages under /root/config/esphome and place the other files there.

