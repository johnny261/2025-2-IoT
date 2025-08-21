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



## 5. Working with the development boards to be studied

When working with a development system, the first thing to do is to get to know it. For this, it is necessary to consult the documentation available such as the user manual, datasheet, examples, and the pinout diagram.

The latter is extremely important because it indicates the names, numbers, and functions of the pins that will be connected to external elements (sensors, actuators, and/or other development systems).  

Knowledge of the pins is also important because it constitutes the starting point for configuring the ports and software modules that will be used in the IoT application in question.

Below are the pinout diagrams for the Arduino UNO and ESP32.

* **Arduino UNO Pinout Map**
  
  ![arduino_uno_pinout](img/arduino_uno-pinout.png)

* **ESP32 Pinout Map**

  ![esp32_pinout](img/nodemcu-esp_32s-pines.jpg)

* **ESP8266 Pinout Map**
  
  ![esp8266_pinout](img/nodemcu_pins.png)

* **Arduino Nano 33 BLE Sense**

  ![arduino_ble_sense](img/arduino_ble_sense.png)

<br/>
<br/>

> **To dive deeper** <br>
For more information about the development systems shown above, check the following [link](https://udea-iot.github.io/UdeA_IoT-page/docs/sesiones/percepcion/sesion2)

---

## 6. Basic Prototyping

### 6.1. Steps to carry out prototyping

A **prototype** is an initial version of the product whose purpose is to provide a tangible and functional representation of the product to identify possible improvements, problems, and gather user feedback.

![prototipado](img/prototipado.png)

In our context, before starting, it is necessary to clearly define the requirements that the electronic system must meet and then determine the components that will be part of the system in question. 

![thinking_design](img/thinking_design.png)

Within the scope we are going to manage, we define the following steps, described below:

1. **Design the circuit**: This involves creating the schematic (for more information see [How to Read a Schematic](https://learn.sparkfun.com/tutorials/how-to-read-a-schematic/)) in which the connection of the components is clearly specified. The following figure shows some common symbols:
   
   ![Esquemático](img/fig-esquematico.png)
   
   Along with the schematic design, we also build the **BOM** (Bill of Materials). A simple template for our case may look like this:

   |Item #|Quantity|Reference|Description|
   |---|---|---|---|
   |1||||
   |2||||
   |...||||

2. **Build the circuit**: Based on the schematic, the circuit is assembled and tested by connecting the different components on a breadboard (for more information see [Breadboards for Beginners](https://learn.adafruit.com/breadboards-for-beginners)).
   
   ![montaje-bb](img/fig-montaje.png)

   Here, the first functional tests are carried out, and the necessary corrections are made before moving on to the final version of the product.

   Sometimes the assembly process is simplified if external modules and expansion boards ([**section 6**](#6-tarjetas-de-expación-y-módulos)) are available, such as the one shown below:

   ![modulo_switch](img/Tactile-Pushbutton-Switch-Module-1.jpg)

3. **Define the list of components**: After the previous step, the next step is to create an inventory of the necessary components known as the **Bill of Materials (BOM)** ([What is a Bill of Materials (BOM) in PCB Design?](https://www.seeedstudio.com/blog/2019/07/24/what-is-a-bill-of-materials-bom-in-pcb-design/)). The following figure (taken from [this link](https://www.proto-electronics.com/blog/how-to-create-best-bom-for-pcb)) shows a typical BOM:
   
   ![BOM](img/BOM_example.png)

4. **Design the PCB prototype**: Once the design has been tested and works according to specifications, the next step is to design the printed circuit board (PCB). For this, PCB design programs such as KiCad or Eagle can be used.
   
   ![pcb](img/fig-pcb.png)

5. **Assemble and test the prototype**: Once the PCB and components are ready, the next step is to solder the components to the PCB and demonstrate the functional product.
   
   ![product](img/Electronic_Product_1.jpeg)
   
   After this, improvements can be carried out through an iterative process to achieve the ideal product.

<br>

> **For further reading**<br>
> If you want to go deeper into the prototyping process, check the following resources:
> 1. **The Essential Guide to Prototyping your Electronic Hardware Product** [[link]](https://www.sparkfun.com/news/3928)  
> 2. **The Essential Guide to Prototyping Your New Electronic Hardware Product** [[link]](https://www.elecrow.com/blog/the-essential-guide-to-prototyping-your-new-electronic-hardware-product.html)  
> 3. **Ultimate Guide: How to Develop and Prototype a New Electronic Hardware Product in 2024** [[link]](https://predictabledesigns.com/how-to-develop-and-prototype-a-new-product/)  
> 4. **7 steps to making a prototype and supercharging your product design** [[link]](https://www.linkedin.com/pulse/7-steps-making-prototype-supercharging-your-product-design-gufhc)  

---

### 6.2. Simple Example

The following example summarizes the procedure above with emphasis on the first three steps. Suppose you want to design a circuit that allows you to turn an LED on and off using a switch.

1. **Design the circuit**: The schematic is shown below:
   
   ![led_sch](img/esquematico-led.jpg)

2. **Build the circuit**: Before assembling the circuit on a breadboard, we will use Fritzing for this:
   
   ![led_bb](img/montaje-bb.jpg)
   
   It is important to note that in the figure above, two possible connections of the same circuit are shown. The idea is to highlight that for the same schematic there can be different assemblies. What truly matters is that the component connections are correct.
   
   Finally, the physical assembly is carried out as shown in the following figure:

   ![led_físico](img/montaje-físico.png)

   Below is the circuit simulated in Tinkercad ([link](https://www.tinkercad.com/things/3xGQvJq9Oq1-ejemploprototipo)):

   ![simulacion](img/simulacion_prototipo.png)

   The simulation in Wokwi ([link](https://wokwi.com/projects/406696186582842369)) is also shown below:

   ![simulacion_wokwi](img/sim_wokwi.png)

3. **Define the list of components**: The list of components for the circuit is shown below:
   
   |Item #|Quantity|Reference|Description|
   |---|---|---|---|
   |1|1|LED1|Red LED|
   |2|1|R1|$330\Omega$ Resistor|
   |3|1|P1|Pushbutton|

To reinforce the above procedure, you are invited to complete the following two exercises.

---

### 6.3. Reinforcement Exercises

#### Exercise 1

The following circuit allows varying the intensity of an LED through a potentiometer connected to an Arduino.  

The list of components is shown in the following BOM:

|Item #|Quantity|Reference|Description|
|---|---|---|---|
|1|1|LED1|Arduino Uno R3|
|2|1|R1|$10k\Omega$ Potentiometer|
|3|1|R2|$270\Omega$ Resistor|

The schematic is shown below:

![sch_ejecicio1](img/ejercicio1.png)

Perform the following tasks:
1. The program to upload to the Arduino UNO is shown below:
   
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
