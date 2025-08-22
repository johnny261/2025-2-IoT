# Implementing a thing

## Objectives

>* Review the basic components of an IoT system
>* Explore the basic components that make up the concept of a thing.
>* Perform initial tests with the ESP32 development board
>* Research the development systems available in the lab.

## Main references

1. Lesson 2 **A deeper dive into IoT** ([link](https://github.com/microsoft/IoT-For-Beginners/blob/main/1-getting-started/lessons/2-deeper-dive/README.md)) form Microsoft's **IoT for Beginners** [[link](https://github.com/microsoft/IoT-For-Beginners)]
2. Lesson 3 **Interact with the phisycal world** ([link](https://github.com/microsoft/IoT-For-Beginners/blob/main/1-getting-started/lessons/3-sensors-and-actuators/README.md)) from Microsoft's **IoT for Beginners** ([link](https://github.com/microsoft/IoT-For-Beginners)).

## 1. Basic components

Within the context of the Internet of Things (IoT), a "thing" refers to any physical device that is connected to the network and can interact with other devices, systems, or services.

The main components of a thing, from a hardware perspective, can be summarized as follows:
1. Transducers (Sensors and actuators)
2. Microcontrollers/Microprocessors
3. Connectivity modules

Let's discuss these in a little more detail.

### 1.1. Sensors and Actuators

Transducers are the elements of the thing that allow the IoT device to interact with the environment. They are the equivalent of the senses in living beings and peripherals in computers.

![Electronic system](img/sistema_electronico.png)

For example, the following figure shows the block diagram of an electronic system that can trigger an alarm when the measured temperature exceeds a certain value.

![Temperature](img/sistema_electronico_ejemplo.png)

Each of these will be discussed in greater detail below.

#### 1.1.1. Sensors

A sensor is a type of transducer whose function is to transform environmental signals (physical signals) into electrical signals, which are the inputs to the system. The following table classifies and summarizes some of the main types of sensors:

![Sensor list](img/sensores_lista.png)

There are several classifications for sensors depending on different criteria, such as the type of environmental signal sensed and the type of electrical signal, among others. Some of these are discussed below.

**Types of Sensors According to the Environmental Signal Sensed**

Sensors can measure many things, from natural properties such as air temperature to physical interactions such as movement. Some existing sensor types are:
* **Temperature sensors**: These can measure the temperature of the air or the medium in which they are immersed. They are sometimes combined with humidity and pressure sensors in a single module.
  
  ![Temperature](img/temperatura.png)

* **Push buttons**: They allow you to sense when they are pressed.
  
  ![Push buttons](img/botones.png)
  
* **Light sensors**: These detect light levels. They also measure different types of light (specific colors, ultraviolet, infrared, or visible light in general).
  
  ![light](img/light.png)

* **Accelerometers**: These allow you to measure movement in multiple directions.
  
  ![acelerometer](img/acelerometro.png)


* **Microphones**: These allow you to detect sounds.
  
  ![microphone](img/microfono.png)


469 / 5.000
**Types of Sensors According to the Electrical Signal**

According to the type of electrical signal obtained at the input, sensors can be classified into two basic types:
* **Analog Sensors**: These are the most basic type of sensors available. These sensors are supplied with voltage (supply voltage) from the IoT device and return (using an **ADC**) a voltage to the device for reading, the variation of which depends on the measured variable.

  ![Trimmer or potentiometer](img/potentiometer.png) 

Below are some examples of this type of sensors:

  ![analog_sensor](img/sensor_análogo.png)

* **Digital Sensors**: Digital sensors detect voltage changes that can only take two possible values (**high** and **low**). The simplest type of this sensor is a **button** or **switch**, which is a sensor with two states: **ON** and **OFF**.
  
  ![Push button](img/button.png) 

  Some examples of this type of sensors are shown below:

  ![digital_sensor](img/sensor_digital.png)

  There are more advanced digital sensors that can sense analog variables thanks to their hardware to process the signal obtained, allowing them to be connected directly to the IoT device. A typical example of this is temperature sensors, which are integrated with an ADC. The analog values obtained are converted into digital signals that are sent to the IoT device as serial data.

  ![serial](img/temperature-as-digital.png)

  The following figure shows some types of these sensors:

  ![digital_sensor2](img/sensor_digital2.png)

  In this type of sensor, data transmission is typically done via a serial protocol. The following list highlights some of the most commonly used ones:

  ![protocols_list](img/protocolos.png)

  Among the most commonly used protocols for IoT are RS-232, I2C, SPI, and OneWire, but we'll discuss these in more detail later.

**Types of Sensors According to Power Supply**

Sensors can be classified based on their power requirements:
* **Active Sensor**: Requires a power source to operate. Some examples include IMUs, LiDAR (Light Detection and Ranging), and CCDs.
* **Passive Sensor**: Does not require power to operate. Some examples include RFID tags, thermistors, and temperature-dependent resistors.

> **To learn more** <br>
> To learn more about sensor terminology, see the following material on sensors ([link](https://udea-iot.github.io/UdeA_IoT-page/docs/sensores-actuadores/sensores/intro)) available in the lecture notes.

#### 1.1.2. Actuators

Actuators perform the opposite task of sensors by converting an electrical signal from the IoT device into an environmental signal intended to interact with the physical world. Some common actuators include:
* **LEDs**: These emit light when turned on.
  
  ![leds.png](img/leds.png)

* **Speaker**: This element emits sound based on the signal it receives, from a basic buzzer to an audio speaker it can be used to play music.
  
  ![speaker](img/speaker.png)

* **Motor**: This converts an electrical signal into a defined rotation.
  
  ![motor](img/motor.png)

* **Relay**: These are switches that can be turned on or off by an electrical signal. These allow small voltages from IoT devices to handle high voltages.
  
  ![relay](img/realy.png)

* **Screens or displays**: These are one of the most complete actuators and display information on a screen. Displays can range from simple LED displays to high-resolution video monitors.
  
  ![display](img/display.png)

**Types of actuators according to the electrical signal**

As with sensors, the type of electrical signal leads to their classification as:
* **Analog actuators**: Analog actuators take an analog signal and convert it into some kind of interaction based on changes in the applied voltage.
  
  ![analog_actuator](img/actuador_análogo.png)

  It's important to note that, like sensors, today's IoT devices work with digital signals, not analog ones. Therefore, to send an analog signal, the IoT device needs an analog-to-digital converter (ADC), which can be integrated into the IoT device or adapted to an external board that connects to it. The ADC will convert the 0s and 1s from the IoT device to an analog voltage that the actuator can use.

* **PWM modulation actuators**: Unlike the use of **ADCs**, another way of converting digital signals to analog signals is through **PWM modulation** which involves sending a train of pulses, the channels act as if they were an analog signal whose amplitude depends on the width of the pulses in the train. A typical example of the use of PWM is the control of the speed of a motor. In this case, the greater the width of the square wave pulse, the higher the speed of the motor.
  
  ![pwm_actuator](img/actuador_pwm.png)

  The following figure shows some cases:

  ![pwm_actuador2](img/actuador_pwm2.png)

* **Digital Actuators**: Similar to digital sensors, digital actuators have two states that are controlled by a **high** and a **low** voltage or have an ADC that allows them to convert an analog signal into a digital one.
  
  ![digital_actuator](img/actuador_digital.png)

  As with sensors, more advanced digital actuators may involve serial communication protocols for connection to the electronic system. 

  ![digital_actuator2](img/actuador_digital2.png)

## 2. Microcontrollers and Microprocessors

As seen in the previous session, microcontrollers and microprocessors are the components of the **thing** responsible for collecting and processing environmental data and performing control actions.

![development_systems](img/sistemas_de_desarrollo.png)

To carry out prototyping work, the elements listed below are available:

|Types|Examples|
|---|---|
|Single-board Computer|<li> Raspberry Pi 4 <li> Raspberry Pi 3 |
|Development boards|<li> Arduino UNO <li> ESP8266 <li> ESP32 <li> ESP32-CAM <li>ARDUINO NANO 33 BLE Sense Lite|

## 3. Connectivity Modules

These allow the IoT device to connect to the network and communicate with other devices or cloud services. These modules can include Wi-Fi, Bluetooth, Zigbee, LoRa, and others.

![connectivity_modules](img/modulos_conexion.png)

La siguiente tabla resume algunos de los principales módulos de acuerdo a la tecnologia:

| Technology | Connectivity Module | Description |
|---------------------|---------------------------------------------------|--------------------------------------------------|
| **Wi-Fi** | ESP8266 | Inexpensive and widely used Wi-Fi module. |
| | ESP32 | Microcontroller with integrated Wi-Fi and Bluetooth. |
| | CC3200 | Wi-Fi module with an ARM Cortex-M4 processor. |
| **Bluetooth** | HC-05 | Classic Bluetooth module, suitable for serial communication. |
| | HC-06 | Similar to the HC-05, but only acts as a slave. |
| | nRF24L01 | Low-cost wireless communication module, based on 2.4 GHz, with support for Bluetooth Low Energy (BLE). |
| **Zigbee** | XBee Series 2 | Zigbee module for mesh networks, widely used in home automation. |
| | CC2530 | Low-power Zigbee SoC for wireless communications. |
| **LoRa** | RFM95W | LoRa module for long-range, low-power communications. |
| | SX1276 | Low-power, long-range LoRa chip used in IoT. |
| **Cellular (2G, 3G, 4G, 5G)** | SIM800 | GSM/GPRS module for 2G cellular communication. |
| | SIM900 | GSM/GPRS module widely used in IoT projects. |
| | Quectel EC25 | 4G LTE module for high-speed cellular communication. |
| **Sub-GHz (915 MHz, 868 MHz)** | RFM69 | RF module for 433/868/915 MHz communications. |
| | CC1101 | Low-power sub-1 GHz transceiver, ideal for sensor networks. |

## 4. Sensors and actuators available in the laboratory

Sensors and actuators are how things interact with their surroundings. There are numerous starter kits on the market. The following modules are available in the laboratory:
* **Grove - Starter Kit v3** [[link]](https://wiki.seeedstudio.com/Grove_Starter_Kit_v3/)
  
  ![kit_groove](img/Grove-Starter_Kit_v2.jpg)

  The following table details the list of components included in this kit:

  |#|Module|Type|
  |---|---|---|
  |1|Grove - LCD RGB Backlight|actuator|
  |2|Grove - Relay|actuator|
  |3|Grove - Buzzer|actuator|
  |4|Grove - Sound Sensor|sensor|
  |5|Grove - Touch Sensor|sensor|
  |6|Grove - Rotary Angle Sensor|sensor|
  |7|Grove - Temperature Sensor|sensor|
  |8|Grove - LED|actuator|
  |9|Grove - Light Sensor|sensor|

> **Documentation**<br>
> For more information, see the documentation **Grove - Starter Kit v3** ([link](https://wiki.seeedstudio.com/Grove_Starter_Kit_v3/))

* **37 Sensor Kit - Elegoo** [[link]](https://www.instructables.com/Arduino-37-in-1-Sensors-Kit-Explained/)
  
  ![elegoo_sensors](img/sensores_elegoo.jpg)

  The list of items for this kit is described below:

  | No. | Module | Type |
  |-----|----------------------------------------|----------|
  | 1   | DHT11 Temperature and Humidity Module  | sensor   |
  | 2   | DS18B20 Temperature Sensor Module      | sensor   |
  | 3   | Button switch module                   | sensor   |
  | 4   | Tilt Switch module                     | sensor   |
  | 5   | IR Transmitter Module                  | actuador |
  | 6   | IR Receiver Module                     | sensor   |
  | 7   | Seven-Color flash Module               | actuador |
  | 8   | Passive Buzzer                         | actuador |
  | 9   | Active Buzzer                          | actuador |
  | 10  | Laser Module                           | actuador |
  | 11  | RGB LED Module                         | actuador |
  | 12  | SMD RGB LED Module                     | actuador |
  | 13  | Photo Interrupter Module               | sensor   |
  | 14  | Two Color LED Module (5mm)             | actuador |
  | 15  | Light Dependent Resistor Module        | sensor   |
  | 16  | Large Microphone Module                | sensor   |
  | 17  | Small microphone module                | sensor   |
  | 18  | Reed Switch Module                     | sensor   |
  | 19  | Digital temperature sensor module      | sensor   |
  | 20  | Linear Magnetic Hall Sensor            | sensor   |
  | 21  | Flame Sensor Module                    | sensor   |
  | 22  | Touch Sensor                           | sensor   |
  | 23  | Seven Color flash Module               | actuador |
  | 24  | Joystick Module                        | sensor   |
  | 25  | Line Tracking Module                   | sensor   |
  | 26  | Obstacle Avoidance Sensor              | sensor   |
  | 27  | Rotary Encode Module                   | sensor   |
  | 28  | Relay Module                           | actuador |
  | 29  | LCD display                            | actuador |
  | 30  | Ultrasonic Sensor Module               | sensor   |
  | 31  | MPU 6050 Module                        | sensor   |
  | 32  | HC SR501 PIR Sensor                    | sensor   |
  | 33  | Water Level Detection Sensor Module    | sensor   |
  | 34  | DS1307 Serial Real Time Clock          | sensor   |
  | 35  | Keypad Module                          | sensor   |

  <br>

  > **Documentation**<br>
  > For more information, consult the documentation of the **Elegoo-sensor-kit** ([link](https://github.com/ieee-uh-makers/elegoo-sensor-kit))

* **Ladzo 37 In 1 Sensors Kit For Arduino** [[link]](https://udea-iot.github.io/UdeA_IoT-page/docs/sensores-actuadores/inventario-lab#landzo-37-in-1-sensors-kit-for-arduino)
  
  ![ladzo_sensors](img/sensores_ladzo.png)

  The list of modules is described below:

  | No. | Module | Type |
  |-----|-----------------------------------|----------|
  | 1   | KY-023 Joystick module            | sensor   |
  | 2   | KY-026 Flame Sensor Module        | sensor   |
  | 3   | KY-016 RGB LED Module             | actuador |
  | 4   | KY-027 2PCS Light Cup module      | sensor   |
  | 5   | KY-003 Hall Magnetic Sensor       | sensor   |
  | 6   | KY-019 Relay Module               | actuador |
  | 7   | KY-024 Linear Hall Sensor         | sensor   |
  | 8   | KY-009 SMD RGB LED                | actuador |
  | 9   | KY-034 7 Color Flash LED          | actuador |
  | 10  | KY-017 Mercury Tilt Switch        | sensor   |
  | 11  | KY-001 18B20 Temperature Sensor   | sensor   |
  | 12  | KY-037 Big Sound Sensor           | sensor   |
  | 13  | KY-036 Touch Sensor               | sensor   |
  | 14  | KY-011 Two Color LED              | actuador |
  | 15  | KY-008 Laser Emitter              | sensor   |
  | 16  | KY-020 Ball Switch                | sensor   |
  | 17  | KY-013 Analog Temperature Sensor  | sensor   |
  | 18  | KY-038 Small Sound Sensor         | sensor   |
  | 19  | KY-028 Digital Temperature Sensor | sensor   |
  | 20  | KY-029 Mini Two-color LED         | actuador |
  | 21  | KY-004 Button                     | sensor   |
  | 22  | KY-018 Photoresistor              | sensor   |
  | 23  | KY-005 IR Emitter                 | actuador |
  | 24  | KY-033 Tracking Sensor            | sensor   |
  | 25  | KY-012 Buzzer                     | actuador |
  | 26  | KY-025 Reed Switch                | actuador |
  | 27  | KY-002 Shock Sensor               | sensor   |
  | 28  | KY-015 Temperature and Humidity Sensor | sensor   |
  | 29  | KY-022 IR Receiver                | sensor   |
  | 30  | KY-032 Avoidance Sensor           | sensor   |
  | 31  | KY-006 Passive Buzzer             | actuador |
  | 32  | KY-021 Mini Reed Switch           | sensor   |
  | 33  | KY-040 Rotary Encoder             | sensor   |
  | 34  | KY-035 Analog Hall Sensor         | sensor   |
  | 35  | KY-031 - Tap Module               | sensor   |
  | 36  | KY-010 - Light blocking           | sensor   |

  <br>

  > **Documentation**<br>
  > Several examples associated with this kit can be found on the page **Arduino | 37 in 1 Sensors Kit Explained** ([link](https://www.instructables.com/Arduino-37-in-1-Sensors-Kit-Explained/))


The following table shows a summary classification of the sensors shown above according to the criteria mentioned in the previous sections:

| Reference COUNTA | | Communication | | | | | | |
|---------------------|-------------------|--------------|--------------|--------------|--------------|-----|--------------|
| Transducer | Reference | 1-Wire | analog | digital | digital + analog | digital + PWM | I2C | Total Sum |
| **Actuator** | | | | | | | | |
| | Active Buzzer | | | x | | | | x |
| | Grove - LCD RGB Backlight | | | | | | x | x |
| | Grove - LED | | | | | x | | x |
| | Grove – Buzzer | | x | | | | | | x |
| | Grove – Relay | | x | | | | | | x |
| | IR Transmitter Module | | | | | x | | x |
| | KY-005 IR Emitter | | x | | | | | x |
| | KY-006 Passive Buzzer | | x | | | | | x |
| | KY-009 SMD RGB LED | | | | | x | | x |
| | KY-011 Two Color LED | | | | | x | | x |
| | KY-012 Buzzer | | x | | | | | x |
| | KY-016 RGB LED Module | | | | | x | | x |
| | KY-019 Relay Module | | x | | | | | x |
| | KY-025 Reed Switch | | x | | | | | x |
| | KY-029 Mini Two-color LED | | | | | x | | x |
| | KY-034 7 Color LED Flash | | x | | | | | x |
| | Laser Module | | | | | x | | x |
| | LCD display | | x | | | | | x |
| | Passive Buzzer | | x | | | | | x |
| | Relay Module | | x | | | | | x |
| | RGB LED Module | | | | | x | | x |
| | Seven Color flash Module | | | | | x | | x |
| | Seven-Color flash Module | | x | | | | | x |
| | SMD RGB LED Module | | | | | x | | x |
| | Two Color LED Module (5mm) | | x | | | | | x |
**Sensor** | | | | | | | | |
| | Button switch module | | x | | | | | x |
| | DHT11 Temperature and Humidity Module | x | | | | | | x |
| | digital temperature sensor module | x | | | | | | x |
| | DS1307 Serial Real Time Clock | | | | | | x | x |
| | DS18B20 Temperature Sensor Module | x | | | | | | x |
| | Flame Sensor Module | | | | | | x | x |
| | Grove - Light Sensor | | x | | | | | x |
| | Grove - Rotary Angle Sensor | | x | | | | | x |
| | Grove - Sound Sensor | | x | | | | | x |
| | Grove - Touch Sensor | | | x | | | | x |
| | Grove – Temperature Sensor | | x | | | | | x |
| | HC SR501 PIR Sensor | | | x | | | | x |
| | IR Receiver Module | | | x | | | | x |
| | Joystick Module | | x | | | | | x |
| | Keypad Module | | | x | | | | x |
| | KY-001 18B20 Temperature Sensor | x | | | | | | x |
| | KY-002 Shock Sensor | | | x | | | | x |
| | KY-003 Hall Magnetic Sensor | | x | | | | | x |
| | KY-004 Button | | | x | | | | x |
| | KY-008 Laser Emitter | | | | | x | | x |
| | KY-010 - Light blocking | | | x | | | | x |
| | KY-013 Analog Temperature Sensor | | x | | | | | x |
| | KY-015 Temperature and Humidity Sensor | x | | | | | | x |
| | KY-017 Mercury Tilt Switch | | | x | | | | x |
| | KY-018 Photoresistor | | x | | | | | x |
| | KY-020 Ball Switch | | | x | | | | x |
| | KY-021 Mini Reed Switch | | | x | | | | x |
| | KY-022 IR Receiver | | | x | | | | x |
| | KY-023 Joystick module | | x | | | | | x |
| | KY-024 Linear Hall Sensor | | x | | | | | x |
| | KY-026 Flame Sensor Module | | | x | | | | x |
| | KY-027 2PCS Light Cup module | | | x | | | | x |
| | KY-028 Digital Temperature Sensor | x | | | | | | x |
| | KY-031 - Tap Module | | | x | | | | x |
| | KY-032 Avoidance Sensor | | | x | | | | x |
| | KY-033 Tracking Sensor | | | x | | | | x |
| | KY-035 Analog Hall Sensor | | x | | | | | x |
| | KY-036 Touch Sensor | | | x | | | | x

## 5. Working with the Development Boards to Study

When working with a development system, the first thing to do is to get to know it. To do this, you need to consult the documentation it provides, such as the user manual, datasheet, examples, and pinout diagram.

The latter is extremely important because it will indicate the names, numbers, and functions of the pins that will be connected to external elements (sensors, actuators, and/or other development systems) on the development systems.

Knowing the pinouts is also important because it constitutes the starting point for configuring the ports and software modules that will be used in the IoT application in question.

Below is the pinout diagram for the Arduino UNO and the ESP32.

* **Arduino UNO pinout map**
  
  ![arduino_uno_pinout](img/arduino_uno-pinout.png)

* **One ESP32 pinout map**

  ![esp32_pinout](img/nodemcu-esp_32s-pines.jpg)

* **Arduino Nano 33 BLE Sense**
  ![arduino_ble_sense](img/arduino_ble_sense.png)

<br/>
<br/>

> **To go deeper** <br>
To go deeper, see the information related to the previous development systems at the following [link](https://udea-iot.github.io/UdeA_IoT-page/docs/sesiones/percepcion/sesion2)

## 6. Basic prototyping

## 6.1. Steps for carrying out prototyping

A **prototype** is an initial version of the product whose purpose is to provide a tangible and functional representation of the product to identify possible improvements, problems, and obtain user feedback.

![prototyping](img/prototipado.png)

In our context, before starting, it is necessary to be clear about the requirements that the electronic system must meet and proceed to determine the components that will be part of the system in question.

![thinking_design](img/thinking_design.png)

Within the scope we will cover, we define some steps, which are described below:

1. **Design the circuit**: This procedure involves designing the schematic (for more in-depth information on this topic, visit the website). [How to Read a Schematic](https://learn.sparkfun.com/tutorials/how-to-read-a-schematic/)) in which the connection of the components is clearly specified. The following figure shows some commonly used symbols:
   
   ![Schematic](img/fig-esquematico.png)
   
   While the schematic design is being carried out, the **BOM** is being built. A simple template for our case could be the following:

   |Item #|Quantity|Reference|Description|
   |---|---|---|---|
   |1||||
   |2||||
   |...||||

2. **Assemble the circuit**: From the schematic, proceed to assemble and test the designed circuit by connecting the different components on a breadboard (for more information consult [Breadboards for Beginners](https://learn.adafruit.com/breadboards-for-beginners)).
   
   ![implementation](img/fig-montaje.png)

   Here, initial functional tests are performed and any necessary corrections are made before moving on to the final version of the product.

   Sometimes the assembly process is reduced by using external modules and expansion cards. ([**section 6**](#6-tarjetas-de-expación-y-módulos)) as shown below:

   ![switch_module](img/Tactile-Pushbutton-Switch-Module-1.jpg)

3. **Define the list of components**: Once the above is done, the next step is to make an inventory of the necessary components known as **Bill of Materials (BOM)** ([What is a Bill of Materials (BOM) in PCB Design?](https://www.seeedstudio.com/blog/2019/07/24/what-is-a-bill-of-materials-bom-in-pcb-design/)). The following figure (taken from the following [link](https://www.proto-electronics.com/blog/how-to-create-best-bom-for-pcb)) shows a tipycall BOM:
   
   ![BOM](img/BOM_example.png)

4. **Designing the prototype PCB**: Once the design is tested and determined to work according to specifications, the printed circuit board is designed. This can be achieved using PCB design software such as KiCad or Eagle.
   
   ![pcb](img/fig-pcb.png)

5. **Assemble and test the prototype**: Once you have the above, what you need to do is solder the components to the PCB and show the functional product.
   
   ![product](img/Electronic_Product_1.jpeg)
   
   After this, further improvements can be made through an iterative process to obtain the ideal product.

<br>

> **To learn more**<br>
> If you'd like to learn a little more about the prototyping process, we invite you to read these pages:
> 1. **The Essential Guide to Prototyping your Electronic Hardware Product** [[link]](https://www.sparkfun.com/news/3928)
> 2. **The Essential Guide to Prototyping Your New Electronic Hardware Product** [[link]](https://www.elecrow.com/blog/the-essential-guide-to-prototyping-your-new-electronic-hardware-product.html)
> 3. **Ultimate Guide: How to Develop and Prototype a New Electronic Hardware Product in 2024** [[link]](https://predictabledesigns.com/how-to-develop-and-prototype-a-new-product/)
> 4. **7 steps to making a prototype and supercharging your product design** [[link]](https://www.linkedin.com/pulse/7-steps-making-prototype-supercharging-your-product-design-gufhc)

### 6.2. Simple Example

The following example summarizes the previous procedure, emphasizing the first three steps. Suppose you want to design a circuit that allows you to turn a device on and off using a switch.

1. **Design the circuit**: The schematic is shown below:
   
   ![led_sch](img/esquematico-led.jpg)

2. **Assembly**: Before assembling the circuit on a breadboard, Wokwi will be used for this:
   
   ![led_bb](img/montaje-bb.jpg)
   
   It's important to note that the previous figure showed two possible connections for the same circuit. The idea is to highlight that different configurations can exist for the same schematic. Regardless of the configuration, the most important thing is that the components are connected correctly.

   Finally, the physical configuration is completed as shown in the following figure:

   ![physical_led](img/montaje-físico.png)

   Below is the simulated circuit in tinkercad ([link](https://www.tinkercad.com/things/3xGQvJq9Oq1-ejemploprototipo)):

   ![simulacion](img/simulacion_prototipo.png)

   Wokwi simulation ([link](https://wokwi.com/projects/406696186582842369)) also shown below:

   ![simulacion_wokwi](img/sim_wokwi.png)


3. **Define the component list**: Below is the circuit component list:

|Item #|Quantity|Reference|Description|
|---|---|---|---|
|1|1|LED1|Red LED|
|2|1|R1|$330\Omega$ resistor|
|3|1|P1|Pushbutton|

To reinforce the previous procedure, we invite you to complete the following two exercises.

### 6.3. Reinforcement Exercises

#### Exercise 1

Below is a circuit that allows you to vary the intensity of an LED using a potentiometer connected to an Arduino.

The component list is shown in the following BOM:


|Item #|Quantity|Reference|Description|
|---|---|---|---|
|1|1|LED1|Arduino Uno R3|
|2|1|R1|Potenciometro de $10k\Omega$|
|3|1|R2|Resistencia de $270\Omega$|


The schematic is shown below:

![Exercice_schematic](img/ejercicio1.png)

Perform the following tasks:
1. The program downloaded to the Arduino UNO is shown below:
   
   ```c++
   const int voltsInPin = A3;
   const int ledPin = 9;

   void setup() {
     pinMode(ledPin, OUTPUT);
   }
   void loop() {
     int rawReading = analogRead(voltsInPin);
     int period = map(rawReading, 0, 1023, 100, 500);
     digitalWrite(ledPin, HIGH);
     delay(period);
     digitalWrite(ledPin, LOW);
     delay(period);
   }
   ```

2. Using [wokwi](https://wokwi.com/), create the setup, write the simulation code, and run the simulation. Then, publish the simulation link to share your work with the community.

#### Exercise 2

The following system shows a simple tone generator. The list of components is shown below:

|Item #|Quantity|Reference|Description|
|---|---|---|---|
|1|1|LED1|Arduino Uno R3|
|2|2|S1, S2|Push button|
|3|1|Sounder|Passive buzzer|

The schematic is shown below:

![Exercice_schematic](img/ejercicio2.png)

Perform the following tasks:
1. Create the assembly in Fritzing and save it as **sounds.fzz**. Then, generate the images associated with the schematic and the assembly.
2. The program downloaded to the Arduino UNO is shown below:
   ```c++
   const int sw1pin = 6;
   const int sw2pin = 7;
   const int soundPin = 8;

   void setup() {
     pinMode(sw1pin, INPUT_PULLUP);
     pinMode(sw2pin, INPUT_PULLUP);
     pinMode(soundPin, OUTPUT);
   }
   void loop() {
     if (!digitalRead(sw1pin)) {
       tone(soundPin, 220);
     }
     else if (!digitalRead(sw2pin)) {
       tone(soundPin, 300);
     }
     else {
       noTone(soundPin);
     }
   }
   ```

3. Using [wokwi](https://wokwi.com/), create the setup, write the simulation code, and run the simulation. Then, publish the simulation link to share your work with the community.

## 7. Expansion Boards and Modules

The prototyping process using a breadboard depends on the complexity of the circuit and the available components. In the worst case, it can be extremely complex (image taken from **BREADBIN IS AN 8-BIT TTL CPU ON A BREADBOARD, IN A BREAD BIN** ([link](https://hackaday.com/2021/10/05/breadbin-is-an-8-bit-ttl-cpu-on-a-breadboard-in-a-bread-bin/))):

![processors](img/procesador_8bits.png)

Fortunately, to save work like this, there are **expansion cards** or **shields** which allow you to connect external components and modules without having to use the breadboard. For example, the **Base Shield V2** ([link](https://wiki.seeedstudio.com/Base_Shield_V2/)):

![base_shield](img/Base_Shield_v2-1.png)

On the other hand, an **external module** consists of one or more hardware components with all the connections and elements necessary to connect the components directly to the ports of a development board or expansion card, without the need for additional hardware. In short, using an external module makes connecting a component practically **plug & play**, eliminating the need for a breadboard and additional wiring. The following figure shows an example where external hardware is used.

![module_connection](img/arduino_servo.png)

In Section 3, some of the **plug & play** modules available in the laboratory were shown. These are characterized as starter modules since the components are not very complex. However, there are more specialized modules such as GPS, transceivers, wireless modules, and higher-precision and higher-power sensors and actuators available.

> **Important** <br>
Using modules and expansion boards facilitates prototyping and saves labor.

There are many manufacturers of modules and expansion boards; some are listed below:

|Manufacturer|Link|
|---|---|
|Adafruit Industries|	https://www.adafruit.com/|
|SparkFun Electronics|	https://www.sparkfun.com/|
|dfrobot|	https://www.dfrobot.com/|
|Seeeed Studio|	https://www.seeedstudio.com/|
|Elegoo| https://www.elegoo.com/|
|sunfounde|https://www.sunfounder.com/|
|robotistan|https://www.robotistan.com/|
|osoyoo|https://osoyoo.com/|
|thingpulse|https://thingpulse.com/
|keyestudio|https://www.keyestudio.com/|
|Arduino|https://store-usa.arduino.cc/products/|

## 8. Arduino Framework

When we talk about Arduino, we're referring to the most popular microcontroller framework today.

Arduino is an open-source electronics platform that combines software and hardware. Since this platform is open hardware, it's possible to use the Arduino programming model to write code for any other Arduino-compatible platform (generic or third-party boards).

The Arduino programming model is based on the **Arduino API**, which presents a set of functions and structures (constants, variables, data types, objects, etc.) that allow the microcontroller to interact with external hardware (sensors and actuators). API information can be found on the Language Reference page. ([link](https://www.arduino.cc/reference/en/)).

![arduino-ref](img/arduino-reference.png)

Before starting it is recommended that you have the document on hand **Arduino Cheat Sheet** ([link](https://github.com/UdeA-IoT/reference-sheets/blob/main/percepcion/arduino/Arduino_Cheat_Sheet.pdf)) from Sparkfun.

## 9. Basic Application Development Using Motherboards

Developing applications involves combining hardware and software knowledge. Regarding the former, in our case, the key is to have a clear understanding of the capabilities of the board to be used and the pinout diagram (for more information, see the following). Regarding software, this knowledge implies knowledge of the C++ language (in our case) and the Arduino Framework programming model.

> **To Go Deeper** <br>
> You can consult the lecture notes, which contain a summary of the most common functions of the Arduino API, in the following section. [link](https://udea-iot.github.io/UdeA_IoT-page/docs/sesiones/percepcion/sesion3)

### 9.1. Caso para el ESP32

Of all the existing boards, the ESP32 will be used ([datasheet](https://cdn.sparkfun.com/datasheets/IoT/esp32_datasheet_en.pdf)). Of the different development platforms for ESP32 that exist, the NodeMCU-32S board from Ai-Thinker is available  ([Nodemcu-32s Datasheet](https://docs.ai-thinker.com/_media/esp32/docs/nodemcu-32s_product_specification.pdf))

![node-mcu](img/nodemcu-32s.png)

To begin, we must first have the card pin diagram on hand, which is shown below:

![ESP32_pins](img/nodemcu_32s_pin.png)

Once this is clear, proceed with the following steps to program the board:
1. Clearly identify the development board pins that will be used to connect external devices (sensors, actuators, etc.). Once this is done, proceed to connect the components.
2. Proceed to program the board using the Arduino programming model (or any other). To do this, use the IDE that best suits you, either the **Arduino IDE** or the **Platformio** extension.
3. Using the IDE, compile and download the program to the development board.
4. Test that the IoT system works according to the requirements defined in the analysis and design stage.

#### Basic I/O on the ESP32

Initially, we will explore the Arduino API to handle basic analog and digital inputs and outputs. As a starting point, you need to be clear about the pins you'll be using and, since they're multifunctional, clearly understand the functions they support. To do this, you need to consult the board's datasheet for the pinout diagram and the functions they can perform. Below, for convenience, we'll show the pinout map for the ESP32 available in the lab:

![NodeMCU_pins](img/nodemcu_32s_pin.png)

The following table shows the board pins classified by functionality:

|Type | Pin Notation (Board)|
|---|---|
|Digital (Only input)|`P34 [GPIO34]`, `P35 [GPIO35]`, `SVP [GPIO36]`, `SVN [GPIO39]`|
|Analog in|`SVP [GPIO36]`, `SVN [GPIO39]`, `P35 [GPIO 35]`, `P34 [GPIO34]`, `P32 [GPIO32]`, `P33 [GPIO 33]`, `P25 [GPIO25]`, `P26 [GPIO26]`, `P27 [GPIO27]`, `P14 [GPIO14]`, `P12 [GPIO12]`, `P13 [GPIO13]`, `P15 [GPIO15]`, `P2 [GPIO2]`, `P0 [GPIO0]`, `P4 [GPIO4]`|
|PWM|`SVP [GPIO36]`, `SVN [GPIO39]`, `P35 [GPIO 35]`, `P34 [GPIO 34]`, `P32 [GPIO 32]`, `P33 [GPIO 33]`, `P25 [GPIO25]`, `P26 [GPIO26]`, `P27 [GPIO27]`, `P14 [GPIO14]`, `P12 [GPIO12]`, `P13 [GPIO13]`, `P15 [GPIO15]`, `P2 [GPIO2]`, `P0 [GPIO0]`, `P4 [GPIO4]`|
|Serial (UART)|`Tx [GPI1]`, `Rx [GPI3]`, `D8 [TXD2]`, `D7 [RXD2]`|
|I2C|`P22 [GPI22/SCL]`, `P21 [GPI21/SDA]`|
|Digital SPI|`P23 [MOSI]`, `P19 [MISO]`, `P18 [SCK]`, `P5 [SS]`|
|Flash SPI|`CLK [GPIO6/FLASHCLK]`, `SD0 [GPIO7/FLASHD0]`, `SD1 [GPIO7/FLASHD1]`, `CMD [GPIO7/FLASHCMD]`, `SD2 [GPIO9/FLASHD2]`, `SD3 [GPIO9/FLASHD3]`|
|Capacitive touch|`P0 [GPIO4]/TOUCH1`, `P4 [GPIO0]/TOUCH0`, `P2 [GPIO2/TOUCH2]`, `P15 [GPIO15/TOUCH3]`, `P13 [GPIO13/TOUCH4]`, `P12 [GPIO12/TOUCH5]`, `P14 [GPIO14/TOUCH6]`, `P27 [GPIO7/TOUCH7]`|

Once you're clear on which pins to use, the next step is to determine the Arduino API functions ([link](https://www.arduino.cc/reference/en/)) that we use to configure and control them. Below are some of the most commonly used ones.

> **For more information** </br> For more information on this, please refer to the page **ESP32 Pinout Reference: Which GPIO pins should you use?** ([link](https://randomnerdtutorials.com/esp32-pinout-reference-gpios/
))

### 9.2. Digital I/O

|Function|Syntax|Description|
|---|---|---|
|[`pinMode()`](https://www.arduino.cc/reference/en/language/functions/digital-io/pinmode/)|`pinMode(pin, mode)`|Configures the pin specified in the `pin` parameter as an input or output. Configuration as an input is done when the `mode` parameter is set to `INPUT`, and as an output when it is set to `OUTPUT`. When a given port has an internal pull-up resistor, it can be configured as an input by setting `mode` to `INPUT_PULLUP` |
|[`digitalWrite()`](https://www.arduino.cc/reference/en/language/functions/digital-io/digitalwrite/)|`digitalWrite(pin)`|Writes a `HIGH` or `LOW` value to the specified `pin` |
|[`digitalRead()`](https://www.arduino.cc/reference/en/language/functions/digital-io/digitalread/)|`int digitalRead(pin)`|Reads the digital value from the specified `pin`, the returned value can be `HIGH` or `LOW`|

### 9.3. Analog I/O

|Function|Syntax|Description|
|---|---|---|
|[`analogRead()`](https://www.arduino.cc/reference/en/language/functions/analog-io/analogread/)|`analogRead(pin)`|Reads the value of an analog pin. The value read depends on the resolution (number of bits) of the selected pin's analog-to-digital converter.|
|[`analogWrite()`](https://www.arduino.cc/reference/en/language/functions/analog-io/analogwrite/)|`analogWrite(pin, value)`|Writes an analog value ([PWM signal](https://docs.arduino.cc/learn/microcontrollers/analog-output/)) to the pin. The PWM signal hardness cycle value (`value`) is a value between `0` and `255`.|

### 9.4. Time

|Function|Syntax|Description|
|---|---|---|
|[`delay()`](https://www.arduino.cc/reference/en/language/functions/time/delay/)|`delay(ms)`|Pauses the program for the amount of time (in milliseconds) specified by the parameter (`ms`)|
|[`delayMicroseconds()`](https://www.arduino.cc/reference/en/language/functions/time/delaymicroseconds/)|`delayMicroseconds(us)`|Pauses the program for the amount of time (in microseconds) specified by the parameter (`us`)|
|[`millis()`](https://www.arduino.cc/reference/en/language/functions/time/millis/)|`time = millis()`|Returns the number of milliseconds that have passed since the board started executing the program.|
|[`micros()`](https://www.arduino.cc/reference/en/language/functions/time/micros/)|`time = micros()`|Gets the number of microseconds that have passed since the board started executing the program.|

### 9.5. Basic Examples Using GPIO

Below are some basic examples that leverage the Arduino I/O API:

**Circuit 1**: Blinking an LED  ([link](https://wokwi.com/projects/357845157032899585))

* **Circuit**:
  
  ![esp32-1](img/montaje1.png)


* **Code**: esp32-ej1.ino
  
  ```cpp 
  void setup() {
    pinMode(LED_BUILTIN, OUTPUT);
  }
  void loop() {
    digitalWrite(LED_BUILTIN, HIGH);   
    delay(1000);                       
    digitalWrite(LED_BUILTIN, LOW);    
    delay(1000);                      
  }
  ```

<br/>

> **Note**: The detailed development of this example can be found in the following [link](ejemplos_GPIO/basic_examples/example1/)

**Circuit 2**: Reading a digital signal  ([link](https://wokwi.com/projects/335034266233602642))

* **Circuit**:
  
  ![esp32-12](img/montaje2.png)


* **Code**: esp32-ej2.ino

    ```cpp
    #define LED_BUILTIN 2
    
    const int buttonPin = 5;         //  (GPIO5 - D5)
    const int ledPin =  LED_BUILTIN; 
    
    // variables will change:
    int buttonState = 0;         
    
    void setup() {
      pinMode(ledPin, OUTPUT);
      pinMode(buttonPin, INPUT);
    }
    
    void loop() {
      buttonState = digitalRead(buttonPin);
    
      if (buttonState == HIGH) {
        digitalWrite(ledPin, HIGH);
      } else {
        digitalWrite(ledPin, LOW);
      }
    }
    ```

<br/>

**Circuit 3**: Handling a PWM signal  ([link](https://wokwi.com/projects/335030762714694227))

* **circuit**:
  
  ![esp32-3](img/montaje3.png)


* **Code**: esp32-ej3.ino

    ```cpp
    int ledPin = 2;    // GPIO2
    
    void setup() {
      // nothing happens in setup
    }
    
    void loop() {
      for (int fadeValue = 0 ; fadeValue <= 255; fadeValue += 5) {
        analogWrite(ledPin, fadeValue);
        delay(30);
      }
    
      for (int fadeValue = 255 ; fadeValue >= 0; fadeValue -= 5) {
        analogWrite(ledPin, fadeValue);
        delay(30);
      }
    }
    ```

<br/>

**Circuit 4**: Reading an analog input  ([link](https://wokwi.com/projects/335035080677261908)).

* **Circuit**:
  
  ![esp32-4](img/montaje4.png)


* **Code**: esp32-ej4.ino

    ```cpp
    const int analogInPin = 15;  //  GPIO15
    const int análogoutPin = LED_BUILTIN; // ESP32 led
    
    int sensorValue = 0;        
    int outputValue = 0;        
    
    void setup() {
      Serial.begin(9600);
    }
    
    void loop() {
      sensorValue = analogRead(analogInPin);
      outputValue = map(sensorValue, 0, 4095, 0, 255); // ADC de 12 bits
      analogWrite(análogoutPin, outputValue);
    
      Serial.print("sensor = ");
      Serial.print(sensorValue);
      Serial.print("\t output = ");
      Serial.println(outputValue);
    
      delay(2);
    }
    ```

<br/>

**Circuit 5**: Debug using the serial port  ([link](https://wokwi.com/projects/358500354708861953)).

One of the most useful applications of the serial port is that it facilitates application debugging. It allows you to print log messages at runtime, which serve to verify the correct operation of the program logic when using a program such as the serial monitor or any similar program. It is very common to print variables (which can indicate the status or value of a sensor, application messages, etc.).

* **Circuit**:
  
  ![esp32-4](img/esp32_debug-serial.png)


* **Code**: 

    ```cpp
    // C++ code

    /* Puertos */

    // Swichtes
    #define SW1 22
    #define SW0 23

    // Leds switches
    #define LED_SW1 21
    #define LED_SW0 19

    // Leds secuencia
    #define LED_PWM 4


    // Potenciometro
    #define POT 2

    /* Variables */
    int pot_value = 0;   // Valor del potenciometro (0 - 2013)
    int val_pwm = 0;     // Valor del pwm (0 - 255)
    int sw_val1;
    int sw_val0;
    int num_seq; 
    int loop_time = 500;

    void inicializar_entradas() {
      // Inicialice aqui las entradas
      pinMode(SW1, INPUT);
      pinMode(SW0, INPUT);
    }

    void inicializar_salidas() {
      // Inicialice aqui las salidas
      pinMode(LED_SW1, OUTPUT);
      pinMode(LED_SW0, OUTPUT);
    }

    void setup() {
      // Inicializacion de las entradas
      inicializar_entradas();
      inicializar_salidas();
      // Debug Serial
      Serial.begin(9600);
      Serial.println("Configuración de I/O -> OK");
    }

    int obtener_numero_secuencia(int sw1, int sw0) {
      // Obtiene el numero asociado a una combinación de switches
      int number;  
      if ((sw1 == LOW)&&(sw0 == LOW)) {
        number = 0;  
      }
      else if ((sw1 == LOW)&&(sw0 == HIGH)) {
        number = 1;
      }
      else if ((sw1 == HIGH)&&(sw0 == LOW)) {
        number = 2;  
      }
      else {
        number = 3;
      }
      //Serial.print("Numero:");
      //Serial.println(number, BIN);
      return number;
    }

    void encender_leds_indicadores(int number) {
      // Encendido de luces indicadores  
      switch(number) {
        case 0:
          digitalWrite(LED_SW1,LOW);
          digitalWrite(LED_SW0,LOW);
          break;
        case 1:
          digitalWrite(LED_SW1,LOW);
          digitalWrite(LED_SW0,HIGH);
          break;
        case 2:
          digitalWrite(LED_SW1,HIGH);
          digitalWrite(LED_SW0,LOW);
          break;
        default:
          digitalWrite(LED_SW1,HIGH);
          digitalWrite(LED_SW0,HIGH);
      }
    }

    void loop() {
      pot_value = analogRead(POT);
      val_pwm = map(pot_value, 0 , 4095, 0, 255);
      analogWrite(LED_PWM,val_pwm);
      Serial.print("POT: ");
      Serial.print(pot_value);  
      Serial.print("; PWM: ");
      Serial.print(val_pwm);
      // Lectura de los switches
      sw_val0 = digitalRead(SW0);  
      sw_val1 = digitalRead(SW1);
      Serial.print("- SW0: ");
      Serial.print(sw_val0);
      Serial.print("; SW1: ");
      Serial.println(sw_val1);
      // Obtencion de la secuencia
      num_seq = obtener_numero_secuencia(sw_val1, sw_val0);  
      // Encendido de los leds
      encender_leds_indicadores(num_seq); 
      delay(loop_time);
    }
    ```

<br/>

> **To go deeper**: To see more things that can be done with the ESP32 you can consult the link within the **randomnerdtutorials** page **160+ ESP32 Projects, Tutorials and Guides with Arduino IDE** ([link](https://randomnerdtutorials.com/projects-esp32/))


A continuación se va a mostrar el procedimiento anterior mediante algunos ejemplos.

### 9.6. Reinforcement Examples

#### Example 1

In [**Exercise 1**](#54-reinforcement-exercises), a manual blinking system using the Arduino UNO was demonstrated:

![exercise1](img/ejercicio1.png)

The originally implemented code is shown below:

```C++
const int voltsInPin = A3;
const int ledPin = 9;

void setup() {
  pinMode(ledPin, OUTPUT);
}
void loop() {
  int rawReading = analogRead(voltsInPin);
  int period = map(rawReading, 0, 1023, 100, 500);
  digitalWrite(ledPin, HIGH);
  delay(period);
  digitalWrite(ledPin, LOW);
  delay(period);
}
```

Reimplement the previous system using the ESP32 and the modules described in the following bill of materials:

|Item #|Quantity|Reference|Description|Information|Remarks|
|---|---|---|---|---|---|
|1|1|LED1|ESP32|||
|2|1|R1|$10kΩ potentiometer|Grove - Rotary Angle Sensor ([link](https://wiki.seeedstudio.com/Grove-Rotary_Angle_Sensor/))|This module is part of the Grove - Starter Kit v3 ([link](https://wiki.seeedstudio.com/Grove_Starter_Kit_v3/))|
|3|1|R2|$1k\Omega$ resistor|Grove - Red LED ([link](https://wiki.seeedstudio.com/Grove-Red_LED/))|This module is part of the Grove - Starter Kit v3 ([link](https://wiki.seeedstudio.com/Grove_Starter_Kit_v3/))|

**Activities**:
- [ ] Rewrite the program to make it work for the ESP32.
- [ ] Simulate the system using [wokwi](https://wokwi.com/)
- [ ] If the simulation is correct, physically connect the system using the components in the table above.
- [ ] Code, compile, and download the program to the ESP32, ensuring that the actual assembly results match the simulation results.
- [ ] Perform this process using the Arduino IDE (See the introductory examples section for the ESP32) by following the steps below. [link](https://udea-iot.github.io/UdeA_IoT-page/docs/sesiones/percepcion/sesion3))

### 9.7. Downloading Applications to the Motherboard

Before you begin, have the NodeMCU pinout diagram ready:

![ESP32_pins](img/nodemcu_32s_pin.png)

Then, depending on the system requirements, clearly determine the pins to be used and their function. Then, proceed to code the program and make the assembly connections. Finally, compile and download the firmware to the board using the appropriate IDE. In our case, we'll discuss the two most commonly used:
* Arduino IDE
* Platformio ([link](../clase3/plaftormio_tutorial/))

## 10. Some application cases

Below is a list of projects that implement some of the aforementioned objectives.

|#|Project|Link|Team|
|---|---|---|---|
|1|Ultrasonic Security System|https://projecthub.arduino.cc/Krepak/ultrasonic-security-system-a6ea3a||
|2|Arduino Calculator|https://projecthub.arduino.cc/123samridhgarg/arduino-calculator-bce0df||
|3|Arduino Solar Tracker|https://projecthub.arduino.cc/Aboubakr_Elhammoumi/arduino-solar-tracker-77347b||
|4|Line Following Robot|https://projecthub.arduino.cc/lightthedreams/line-following-robot-34b1d3||

## 11. Additional Examples

### 11.1. Examples Using an RGB LED

1. Connect an RGB LED to the ESP32 and set it to light up using different colors [[[simulation]](https://wokwi.com/projects/391210532094486529) | [[solution]](ejemplos_GPIO/RGB_example/example1/README.md)].
   
   ![RGB_1](img/ESP32_RGB_1.png)

2. Connect an RGB LED to the ESP32 and set it to light up, changing to a different color each time the user presses a button. [[[simulation]](https://wokwi.com/projects/391344633629636609) | [[solution]](ejemplos_GPIO/RGB_example/example2/README.md)].
   
   ![RGB_2](img/ESP32_RGB_2.png)

### 11.2. Examples using a PIR sensor

1. Activate an LED when presence is detected using a PIR sensor
  [[[simulation]](https://wokwi.com/projects/391364172928279553) | [[solution]](https://github.com/UdeA-IoT/clases-IoT_2024-2/blob/main/clase4/ejemplos_GPIO/PIR_example/example1/README.md)]
   
   ![PIR_1](img/ESP32_PIR_example1.png)

2. Activate an LED when a presence is detected using a PIR sensor. In addition to the light signal used to indicate presence, the system will have a buzzer to generate an audible alarm. This audible alarm can be deactivated or activated using a push button.
 [[[simulation]](https://wokwi.com/projects/391364988125921281) | [[solution]](https://github.com/UdeA-IoT/clases-IoT_2024-2/blob/main/clase4/ejemplos_GPIO/PIR_example/example2/README.md)]
   
   ![PIR_2](img/ESP32_PIR_example2.png)


### 11.3. Examples using an ultrasonic sensor

1. This example was adapted from **SparkFun Inventor's Kit Experiment Guide - Project 3: Motion** ([link](https://learn.sparkfun.com/tutorials/sparkfun-inventors-kit-experiment-guide---v40/project-3-motion)) for ESP32
 [[[simulation]](https://wokwi.com/projects/391349504507707393) | [[solution]](https://github.com/UdeA-IoT/clases-IoT_2024-2/blob/main/clase4/ejemplos_GPIO/ultrasonic-sensor_example/example1/README.md)]. 
   ![ultrasound_1](img/esp32-ultrasonido_1.png)
  
2. The following example shows, using the serial monitor, the distance in centimeters and inches, which was implemented in the previous example with an LED that changes color as the distance measured by the ultrasonic sensor changes.
 [[[simulation]](https://wokwi.com/projects/391350736522728449) | [[solution]](https://github.com/UdeA-IoT/clases-IoT_2024-2/blob/main/clase4/ejemplos_GPIO/ultrasonic-sensor_example/example2/README.md)]
    ![ultrasonido_2](img/esp32-ultrasonido_2.png)

## 12. About Components

### 12.1. Manufacturers

The following table shows some of the main companies dedicated to manufacturing modules for IoT prototyping:

|Manufacturer|Link|
|---|---|
|Adafruit Industries|https://www.adafruit.com/|
|SparkFun Electronics|https://www.sparkfun.com/|
|dfrobot|https://www.dfrobot.com/|
|Seeeed Studio|https://www.seeedstudio.com/|
|Elegoo|https://www.elegoo.com/|

In addition to manufacturing, they also document and show demonstrative examples of how to use the components manufactured there.

### 12.2. Distributors

If you want to buy electronic components, there are distributors for that. The following table shows some of the main component distributors worldwide (taken from the website **2023 Top 50 Electronics Distributors List** ([link](https://www.supplychainconnect.com/rankings-research/article/21264998/2023-top-50-electronics-distributors-list))):

|Distributors|Link||---|---|
|Mouser Electronics|https://www.mouser.com/|
|DigiKey Corporation|https://www.digikey.com/|
|Arrow Electronics|https://www.arrow.com/|
|WPG Holdings|https://www.wpgholdings.com/main/index/en|
|Avnet|https://www.avnet.com/wps/portal/us/|
|Future Electronics|https://www.futureelectronics.com/|

In the Colombian case, the following list (taken from the forum **List of Electronics Suppliers - Colombia** ([link](https://www.forosdeelectronica.com/resources/listado-de-proveedores-de-electr%C3%B3nica-colombia.105/))) contains some of the distributors in Colombia:

|Distributors|Link|
|---|---|
|I + D|https://didacticaselectronicas.com/|
|Sigma Electronica|https://www.sigmaelectronica.net/|
|Electronilab|https://electronilab.co/|
|Suconel|https://suconel.com/|
|La Red Electronica|https://laredelectronica.com/|

## 13. Activity

If you don't remember, review the **platformio Tutorial** ([link](../clase3/platformio_tutorial/)), which shows the procedure for downloading a program to the ESP32. Then, try to understand the basic examples shown in the following [link](ejemplos_GPIO/README.md). The objective of these is to train you in the procedure previously shown for downloading firmware to the card.

Once you understand the examples shown above, perform the following tasks:
1. To do this, create a directory called **exampleX** (where X is the number of the example that will be added to the sequence).
2. Copy and paste the following template ([link](template/README.md)) into the created directory and modify it according to the description given there. For this, you can use the [example1](example1/) directory as a base.
3. Perform the download procedure on the ESP32 using Platformio. Take a photo of the physical assembly and attach it to the created directory. Make a YouTube video of the assembly in operation. Finally, adapt the template by attaching the necessary resources (Fritzing file, schematic and assembly image, source code, directory with the source code generated by Platformio), the photo in the repo, and the YouTube video link showing the actual operation.

## 14. Resources to go further

Explore the following sites to get an idea of what can be done:
* https://randomnerdtutorials.com/
* https://www.adafruit.com/
* https://www.sparkfun.com/
* https://www.seeedstudio.com/
* https://www.luisllamas.es/
* https://www.hackster.io/
* https://hackaday.com/
* https://projecthub.arduino.cc/
* https://makezine.com/
* https://make.co/
* https://es.ubidots.com/
* https://www.wildernesslabs.co/


## 15. References

* https://how2electronics.com/10-essential-iot-starter-kits-to-kickstart-your-journey/
* https://github.com/UdeA-IoT/actividad-4
* https://udea-iot.github.io/UdeA_IoT-page/docs/sensores-actuadores/sensores/intro
* https://gist.github.com/lyqht
* https://github.com/microsoft/IoT-For-Beginners
* https://github.com/microsoft/ML-For-Beginners
* https://github.com/microsoft/Web-Dev-For-Beginners
* https://github.com/microsoft/ai-for-beginners
* https://github.com/microsoft/Data-Science-For-Beginners
* https://digitalconcepts.net.au/fritzing/index.php?op=parts
* https://www.studiopieters.nl/fritzing/
* https://codeadam.ca
* https://github.com/Intelligent-Internet-of-Things-Course
* https://github.com/ETSISI-CCforIoT
* https://azure.github.io/IoTTrainingPack/
* https://github.com/orgs/programming-the-iot/repositories
* https://github.com/antmicro/dl-in-iot-course

