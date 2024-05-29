# Amrit-Raj/Aditya-Manjunath/HighRiders


# IoT Health Monitor

This project is about designing an IoT health monitor to track heart rate and SpO2 (blood oxygen saturation) using the VSDSquadron Mini RISC-V development board. It involves interfacing suitable sensors with the board and ensuring data can be processed and transmitted effectively.

## Components Needed
1. **VSDSquadron Mini RISC-V Development Board**
2. **Heart Rate and SpO2 Sensor**: MAX30100 or MAX30102
3. **Display**: OLED Display (optional for local display of data)
4. **Communication Module**: WiFi module like ESP8266 or Bluetooth module like HC-05 (for IoT capabilities)
5. **Power Supply**: Battery or USB power source
6. **Connecting Wires**

## Interfacing Diagram

Below is the interfacing diagram for connecting the MAX30100 sensor and an optional OLED display to the VSDSquadron Mini board and the ESP8266 for WiFi communication.

## Components Pin Connections

### MAX30100 Sensor

| Pin           | VSDSquadron Mini Board Pin        |
|---------------|-----------------------------------|
| SDA           | GPIO2 (I2C SDA)                   |
| SCL           | GPIO3 (I2C SCL)                   |
| INT (Optional)| GPIO4 (Optional for interrupt-based reading) |
| VIN           | 3.3V (Power)                      |
| GND           | GND (Ground)                      |

### OLED Display (Optional)

| Pin           | VSDSquadron Mini Board Pin        |
|---------------|-----------------------------------|
| SDA           | GPIO2 (I2C SDA)                   |
| SCL           | GPIO3 (I2C SCL)                   |
| VIN           | 3.3V (Power)                      |
| GND           | GND (Ground)                      |

### ESP8266 WiFi Module

| Pin           | VSDSquadron Mini Board Pin        |
|---------------|-----------------------------------|
| TX            | GPIO5 (UART RX)                   |
| RX            | GPIO6 (UART TX)                   |
| CH_PD         | 3.3V (Power)                      |
| VCC           | 3.3V (Power)                      |
| GND           | GND (Ground)                      |


### Interfacing Diagram
![](circuit_diagram.jpg)
