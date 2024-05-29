# Amrit-Raj/Aditya-Manjunath/HighRiders


# IoT Health Monitor
## Introduction
The IoT-based health monitor is designed to efficiently track heart rate and SpO2 (blood oxygen saturation) using the VSDSquadron Mini RISC-V development board and the MAX30100 sensor. This system enables continuous monitoring and data transmission through the ESP8266 WiFi module, allowing for remote health tracking via cloud platforms. Optional integration with an OLED display provides local data visualization. This technology offers a scalable and adaptable solution for personal and clinical health monitoring, leveraging advanced sensors and IoT capabilities to deliver real-time insights and long-term health data analysis

## Overview
This project focuses on developing an IoT-based health monitor to track heart rate and SpO2 (blood oxygen saturation). Utilizing the VSDSquadron Mini RISC-V development board and the MAX30100 sensor, the system is designed to provide continuous monitoring of vital signs. The integration with an ESP8266 WiFi module enables real-time data transmission to cloud platforms like ThingSpeak or AWS IoT, facilitating remote health tracking and long-term data analysis. An optional OLED display allows users to view their health metrics locally. The project involves interfacing the components through I2C and UART connections, ensuring efficient data processing and transmission. The software implementation includes sensor initialization, data acquisition, processing, and communication with the cloud. This scalable and adaptable system is suitable for various applications, from personal health tracking to clinical environments, offering a comprehensive solution for modern healthcare needs.

## Components Needed
1. **VSDSquadron Mini RISC-V Development Board**
2. **Heart Rate and SpO2 Sensor**: MAX30100 or MAX30102
3. **Display**: OLED Display (optional for local display of data)
4. **Communication Module**: WiFi module like ESP8266 or Bluetooth module like HC-05 (for IoT capabilities)
5. **Power Supply**: Battery or USB power source
6. **Connecting Wires**


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


### Circuit Connection Diagram
![](circuit_diagram.jpg)
