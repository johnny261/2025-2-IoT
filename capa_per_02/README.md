# Basic Components of an IoT System

## Objectives

>* Make the first tests with the ESP32 development board  
>* Use simple circuits and programs with an online simulator for the platform  

## Main References

1. Lesson 2 **A deeper dive into IoT** ([link](https://github.com/microsoft/IoT-For-Beginners/blob/main/1-getting-started/lessons/2-deeper-dive/README.md)) from Microsoft’s **IoT for Beginners** course [[link](https://github.com/microsoft/IoT-For-Beginners)]
2. Lesson 3 **Interact with the physical world** ([link](https://github.com/microsoft/IoT-For-Beginners/blob/main/1-getting-started/lessons/3-sensors-and-actuators/README.md)) from Microsoft’s **IoT for Beginners** ([link](https://github.com/microsoft/IoT-For-Beginners)).

## Online Simulators

The following is a list of applications that will be used for simulation purposes. To use them, just have a Google email account, for example:
- [x] Tinkercad (https://www.tinkercad.com/)
- [x] Wokwi (https://wokwi.com/)

## Classroom Work

## 1. Development Systems

The heart of IoT systems is the things. They are responsible for enabling the system’s interaction with the environment by collecting, processing data, and performing control actions over it.  

To carry out prototyping tasks, development systems (dev kits) are used, which are of two types *Microcontrollers* and *Single Board Computers* as shown in the following figure:

![dev_kits](img/dev_kids.png)

### Systems available in the laboratory

Below is a list of some development systems. Those available in the laboratory are marked.

#### Microcontrollers

- [x] Arduino UNO 
- [x] ESP8266 
- [x] ESP32 
- [x] ARDUINO NANO 33 BLE Sense Lite

#### Single Board Computers

- [x]  Raspberry Pi [[link]](https://www.raspberrypi.com/) 
- [ ]  BeagleBoard [[link]](https://www.beagleboard.org/) 
- [ ]  Orange Pi [[link]](http://www.orangepi.org/)  
- [ ]  Banana Pi [[link]](https://www.banana-pi.org/)  
- [ ]  Intel Galileo [[link]](https://ark.intel.com/content/www/us/en/ark/products/78919/intel-galileo-board.html)

> **To go deeper** <br>
> To learn more about these elements available in the laboratory check the following [link](https://udea-iot.github.io/UdeA_IoT-page/docs/sesiones/percepcion/sesion2)

## 2. Development environment configuration for microcontrollers

### Arduino framework

To program a microcontroller, some tools are needed to develop the software that will run on the microcontroller (firmware). Due to the large number of existing microcontrollers, each manufacturer offers a framework to facilitate the development of applications for any compatible microcontroller.  

Due to its popularity and ease of use, in this course we will use the Arduino Framework. Arduino is an open-source electronics platform that combines hardware and software, making it ideal for programming not only Arduino boards, but also boards from other manufacturers using the programming model employed in Arduino.  

In this model, the boards are programmed in C or C++ using a code file known as a **sketch** ([link](https://github.com/microsoft/IoT-For-Beginners/blob/main/1-getting-started/lessons/2-deeper-dive/README.md)):

![arduino-skech](img/arduino-sketch.png)

The **sketch** consists of two main functions (see figure taken from the following [link](https://github.com/microsoft/IoT-For-Beginners/blob/main/1-getting-started/lessons/2-deeper-dive/README.md)):
* **`setup`**: Initialization code (port initialization, Wi-Fi connection, cloud services, etc.) that runs when the microcontroller is powered on. 
* **`loop`**: Code that runs continuously while the microcontroller is on. This is where the application logic is implemented (sensor reading, actuator control, sending and receiving information, etc).

Below is a typical code template:

```cpp
// Project Name
// Description: Brief description of the project and its functionality

// Include necessary libraries
#include <Arduino.h>

// Define constants and pin assignments

// Global variables

void setup() {
    // Initial setup
    // code...
}

void loop() {
    // Code that runs repeatedly
    // code...
}
