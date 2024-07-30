# Automated Greenhouse Project

## Overview

This project is an automated greenhouse system designed for efficient plant cultivation. The core of the system is based on the ESP32 microcontroller (specifically, ESP32-DevKitC-02), capable of reading data from various sensors and controlling actuators. The project leverages a modular and scalable architecture, allowing users to easily extend and customize the system with additional sensors and actuators, without the need to re-write code for each new component. Currently, the project works only with DHT11 sensors.

## Features

- **Modular Design:** The project is built upon a modular architecture, utilizing interface classes for sensors and actuators. This design allows for seamless scalability without the need to rewrite code for each new component.
- **Scalability:** Easily expand the system by adding new sensors or actuators.
- **Web Server:** The system sends sensor data to a server, which is hosted by the ESP, for remote monitoring and data analysis.

## Getting Started

Follow these steps to set up and customize the automated greenhouse system:

1. **Hardware Setup:** Connect your sensors (DHT11, Analog Sensors), actuators (12V DC-water pump, 12V DC-fan, 5V-servo), and any additional components as per the provided circuit diagram.

2. **Configuration:** Open the `config.h` file to declare new sensors or actuator objects. In `config.cpp` define the declared variables.

3. **Web Server Setup:** Configure your WiFi credentials in `config.cpp` to enable data transmission to the web server.

4. **Upload Code:** Upload the code to the ESP32 microcontroller using your preferred development environment.

## Adding New Components

There are two types of components. Sensors and Motors.
A sensor object can be an analog sensor for humidity, or a DHT sensor for temperature. 
A motor object can be a servo or a DC motor. For the motors it is required to use an external power supply and control them with relays, to avoid damaging the μC. 
In this project a 12V DC motor is being used as a water pump, a 12V DC fan for heat control and a 5V servo for opening/closing a window. 

To add new sensors or actuators to the system:

1. Create a new object derived from the corresponding interface class (`Sensor` or `Motor`). It can be a `DHTSensor`, `HMDSensor` or `Fan`, `Pump`, `Servo`. 
2. Declare the necessary attributes for the new components in the `config.h` file.
3. Define the components in `config.cpp` file. 

```cpp
// "config.h"
// Example for adding a new DHT11 sensor
// DHT Sensor parameters config.h
extern float DHT_THRESHOLD;

// DHT Sensor N
extern const uint8_t DHT_N_TYPE_CONFIG;        // DHT11
extern const uint8_t DHT_N_DATA_PIN_CONFIG;    // The data pin you have connected the sensor to the ESP. N: sensor index
extern DHTSensor dhtSensor_N;                // The new component as an object. (e.g dhtSensor1, dhtSensor2, ...).


// "config.cpp"
// DHT Sensor parameters 
float DHT_THRESHOLD = 26;

// DHT Sensor N
const uint8_t DHT_N_TYPE_CONFIG = DHT11;
const uint8_t DHT_N_DATA_PIN_CONFIG{6};
DHTSensor dhtSensor1(DHT_N_DATA_PIN_CONFIG, DHT_N_TYPE_CONFIG);

