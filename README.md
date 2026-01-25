# ESPHome Projects

- [Water Meter](#water-meter)
- BLE Tracker

## Water Meter
Source: https://github.com/tronikos/esphome-magnetometer-water-gas-meter

### Components
- [Wemos D1 mini clone (ESP8266)](https://www.aliexpress.us/item/3256807691590176.html)
- [GY-271 Magnetometer (QMC5883P)](https://www.aliexpress.us/item/3256806634225105.html) - I2C address: 0x2C
- Cat-5e ethernet cable

### Wiring

| D1 mini | GY-271 | 
|---|---|
| 3V3 |  VCC |
| G   |  GND |
| D1  |  SCL |
| D2  |  SDA |

### Setup

Remember to run calibrate axis with water running, and check logs in ESPHome to confirm it was successful. 

Exposed sensors in HA:
```
sensor.water_meter_flow
sensor.water_meter_total  
```

Other helpers:
```
sensors:
  - platform: statistics
    name: "Water Usage Last 24 Hours"
    unique_id: water_usage_last_24_hours
    entity_id: sensor.water_meter_total
    state_characteristic: change
    max_age:
        hours: 24

utility_meter:
  water_usage_daily:
    name: Water Usage Daily
    unique_id: water_usage_daily
    source: sensor.water_meter_total
    cycle: daily
  water_usage_weekly:
    name: Water Usage Weekly
    unique_id: water_usage_weekly
    source: sensor.water_meter_total
    cycle: weekly
  water_usage_monthly:
    name: Water Usage Monthly
    unique_id: water_usage_monthly
    source: sensor.water_meter_total
    cycle: monthly
  water_usage_yearly:
    name: Water Usage Yearly
    unique_id: water_usage_yearly
    source: sensor.water_meter_total
    cycle: yearly
```