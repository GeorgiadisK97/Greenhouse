# Automated Greenhouse Project

## Overview

This project is an automated greenhouse system designed for efficient plant cultivation. The core of the system is based on the ESP32 microcontroller (specifically, ESP32-DevKitC-02), capable of reading data from various sensors and controlling actuators. The project leverages a modular and scalable architecture, allowing users to easily extend and customize the system with additional sensors and actuators, without the need to re-write code for each new component. Currently, the project works only with DHT11 sensors.

## Features

- **Modular Design:** The project is built upon a modular architecture, utilizing interface classes for sensors and actuators. This design allows for seamless scalability without the need to rewrite code for each new component.

- **Scalability:** Easily expand the system by adding new sensors or actuators. The scalability is achieved through a configuration file (`config.h`), where users can define new objects and with their corresponding attributes.

- **Web Server:** The system sends sensor data to a server, which is hosted by the ESP, for remote monitoring and data analysis.

## Getting Started

Follow these steps to set up and customize the automated greenhouse system:

1. **Hardware Setup:** Connect your sensors (DHT11, soil moisture), actuators (12V DC-water pump, 12V DC-fan, 5V-servo), and any additional components as per the provided circuit diagram.

2. **Configuration:** Open the `config.h` file to add new sensors or actuator objects. Enter your desired values for each.

3. **Web Server Setup:** Configure your WiFi credentials in the code to enable data transmission to the web server.

4. **Upload Code:** Upload the code to the ESP32 microcontroller using your preferred development environment.

## Adding New Components

To add new sensors or actuators to the system:

1. Create a new object derived from the corresponding interface class (`Sensor` or `Motor`).
2. Declare the necessary attributes for the new components in the `config.h` file.
3. Define the components in `config.cpp` file. 

```cpp
// Example for adding a new DHT11 sensor
// DHT Sensor parameters Config.h
extern const uint8_t DHT_TYPE_Ν_CONFIG;        // DHT11 or DHT22
extern const uint8_t DHT_DATA_PIN_N_CONFIG;    // The data pin you have connected the sensor to the ESP. N: sensor index
extern float DHT_THRESHOLD;
extern float OFFSET;
extern DHTSensor dhtSensorN;                // The new component as an object. (e.g dhtSensor1, dhtSensor2, ...).

// DHT Sensor parameters Config.cpp
const uint8_t DHT_TYPE_N_CONFIG = DHT11;
const uint8_t DHT_DATA_PIN_N_CONFIG{6};
float DHT_THRESHOLD = 26;
float OFFSET{1};
DHTSensor dhtSensor1(DHT_DATA_PIN_CONFIG, DHT_TYPE_CONFIG);

