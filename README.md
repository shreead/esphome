# ESPHome Projects

### Setup
- [ESPHome Docker](#esphome-docker)

### Projects
- [Water Meter](config/water-meter.md)
- [ESP32-CAM](config/esp32-cam.md)
- BLE Tracker

---

## ESPHome Docker
```yaml
services:
  esphome:
    container_name: esphome
    image: esphome/esphome
    volumes:
      - ./config:/config
      - /etc/localtime:/etc/localtime:ro
    restart: always
    # privileged: true # needed if passing through USB port
    network_mode: host
```

Can be accessed at http://IP:6052
