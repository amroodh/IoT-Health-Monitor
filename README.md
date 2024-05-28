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
```plaintext
            +------------------------+
            | VSDSquadron Mini Board |
            |                        |
            | 3.3V ----------------+ |
            | GND ---------------+ | |
            |                    | | |
            | GPIO2 (I2C SDA) ---|-|-|----> MAX30100 SDA
            | GPIO3 (I2C SCL) ---|-|-|----> MAX30100 SCL
            | GPIO4 (INT) -------|-|-|----> MAX30100 INT (Optional)
            |                    | | |
            | GPIO5 (UART RX) ---|-|-|----> ESP8266 TX
            | GPIO6 (UART TX) ---|-|-|----> ESP8266 RX
            |                    | | |
            +------------------------+
                     |  |
                     |  |
           +---------+  +-------------+
           |                          |
      +----+----+                +----+----+
      | MAX30100 |                | ESP8266 |
      |          |                |         |
      +---------+                +---------+
         |  |
         |  |
         +--+

```
### Working Code
```
#include <Wire.h>
#include <MAX30100.h>
#include <SoftwareSerial.h>

#define I2C_SDA 2
#define I2C_SCL 3
#define UART_RX 5
#define UART_TX 6

MAX30100 sensor;
SoftwareSerial esp8266(UART_RX, UART_TX);

void setup() {
    Wire.begin(I2C_SDA, I2C_SCL);
    Serial.begin(115200);
    esp8266.begin(115200);

    sensor.begin();
    sensor.setMode(MAX30100_MODE_SPO2_HR);
    sensor.setLedsPulseWidth(MAX30100_SPC_PW_1600US_16BITS);
    sensor.setSamplingRate(MAX30100_SAMPRATE_100HZ);
    sensor.setHighresModeEnabled(true);
}

void loop() {
    sensor.update();

    if (sensor.getRawIRValue() > 50000) {
        float hr = sensor.getHeartRate();
        float spo2 = sensor.getSpO2();
        
        Serial.print("Heart Rate: ");
        Serial.print(hr);
        Serial.print(" BPM SpO2: ");
        Serial.print(spo2);
        Serial.println(" %");
        
        esp8266.print("AT+CIPSTART=\"TCP\",\"api.thingspeak.com\",80\r\n");
        delay(2000);
        esp8266.print("AT+CIPSEND=40\r\n");
        delay(2000);
        esp8266.print("GET /update?api_key=YOUR_API_KEY&field1=");
        esp8266.print(hr);
        esp8266.print("&field2=");
        esp8266.print(spo2);
        esp8266.print("\r\n");
        delay(2000);
    }

    delay(1000);
}
```
