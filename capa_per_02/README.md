# Implementing a Thing

## Objectives

>* Review the basic components of an IoT system
>* Explore the basic components that make up the concept of a "thing".
>* Perform the first tests with the ESP32 development board
>* Investigate the development systems available in the laboratory.

## Main References

1. Lesson 2 **A deeper dive into IoT** ([link](https://github.com/microsoft/IoT-For-Beginners/blob/main/1-getting-started/lessons/2-deeper-dive/README.md)) from the Microsoft course **IoT for Beginners** [[link](https://github.com/microsoft/IoT-For-Beginners)]
2. Lesson 3 **Interact with the physical world** ([link](https://github.com/microsoft/IoT-For-Beginners/blob/main/1-getting-started/lessons/3-sensors-and-actuators/README.md)) from Microsoft’s **IoT for Beginners** course ([link](https://github.com/microsoft/IoT-For-Beginners)).

## 0. Arduino IDE Configuration
1. Go to this [link](https://www.arduino.cc/en/software), download and install the software.

2. Once installed, go to File -> Preferences -> Manage additional boards and insert this link into the box:

[https://espressif.github.io/arduino-esp32/package_esp32_index.json](https://espressif.github.io/arduino-esp32/package_esp32_index.json)

This step is necessary for the IDE to recognize the boards developed for the ESP32.

![Arduino ESP32 Configuration](img/Arduino-Prefs.png)

3. Install the ESP32 boards in the Arduino IDE.  
   1. Select Boards, 2. Search for "esp", 3. Install them.

![ESP32 boards installation](img/ESP32-boards.png) 

4. In the Arduino IDE, look for the appropriate board for your microcontroller using the menu:

Tools -> Boards -> ESP32

5. Connect the microcontroller to the computer. The computer should recognize it as a COMxx port (in Windows) or a /dev/ttySxx port (in Linux).

6. In the Arduino IDE, look for the correct port for your microcontroller using the menu:

Tools -> Port -> \[Choose the port here\]

![Port Configuration](img/Arduino-Port.png)

6. Insert the code from the image, compile the code (1), upload the program to the microcontroller (2), and open the serial monitor (3).

![Serial Test](img/Arduino-TestSerial.png)
