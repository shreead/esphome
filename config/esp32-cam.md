# ESP32-CAM


## Hardware
- [ESP32-CAM](https://www.amazon.com/dp/B08P2578LV) with these specifications:
    - OV2640 camera ([datasheet](https://dl.espressif.com/dl/schematics/Camera_OV2640.pdf)): 1600x1200 (2MP), 15fps
    - ESP32-S board
    - SPIFlash: Default 32Mbit
    - RAM: Internal 520KB + external 4MB PSRAM
    - Micro USB to Serial Port CH-340G


## ESPHome configuration
Uses the following components
- esp32_camera: use the Ai-Thinker Camera configuration example
- esp32_camera_web_server: to provide direct link for snapshots
- light: for on board "Flash Lamp"


## Upload to device
According to documentation you need to press the IO0 button (aka "Download" button) when connecting to the USB to computer, but didn't work for me, so I flashed it via esphome CLI
```
esphome run esp32-cam.yaml
```
and then choose upload over USB. 


## Home Assistant
Esposes the following:
```
camera.esp32_cam_camera
light.esp32_cam_flash_lamp
```


## Web Server
`http://\<IP\>:8081` downloads snapshot as timestamp.jpg file


## Pinout
Some info about GPIO pins:
- 16 is safest
- 0 - high is boot, low to flash. 
- 4 is white LED
- 33 builtin LED, inverted
- 2,4,12-15 can't be used if SD card is connected


## References
- https://esphome.io/components/esp32_camera/
- https://dl.espressif.com/dl/schematics/Camera_OV2640.pdf
- https://jamesachambers.com/cheap-esp32-cam-home-assistant-esphome-camera-guide/
- https://lastminuteengineers.com/esp32-cam-pinout-reference/
