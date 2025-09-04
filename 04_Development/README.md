# A review of firmware development

## Objectives

>* Getting close to some alternatives to develop firmware for MCUs
>* Apply some of this strategies in a simple example. 
>* Keep going with the relationship with the embedded plattform.

## State Machines

A state machine or *Finite State Machine (FSM)* can be defined as:

```
It's a computational abstraction. A model of the behavior of an automatic machine. This model uses States, Transitions, Inputs and Outputs.
```

They are widely used in the development of small/medium complexity applications. For example, the image shows a FSM example for cleaning up items in a household.

![state_machine](img/fsm_example.svg)

FSMs start a well knew point and, while inputs (or conditions) are changing, the FSM decides wich state is the next to be executed (transitions).

### Example # 1

Let's make a simple semaphore controller using FSM methodology, the state diagrams looks like this:

![fsm_semaphore](img/fsm_semaphore.png)

The code should look similar to this:

```Arduino
#include <Arduino.h>

// Pins for leds and button
#define L_G  26
#define L_Y  27
#define L_R  25
#define BUT  14

// States of the FSM
#define ST_GREEN  0
#define ST_YELLOW 1
#define ST_RED    2

int curr_state = ST_GREEN;

// State times
unsigned long tbefore = 0;
const unsigned long green_interval = 5000;    // 5s
const unsigned long yellow_interval = 2000; // 2s
const unsigned long red_interval = 5000;     // 5s

// Function to manage FSM
void fsm_process();

void setup()
{
    pinMode(L_G, OUTPUT);
    pinMode(L_Y, OUTPUT);
    pinMode(L_R, OUTPUT);
    pinMode(BUT, INPUT_PULLUP);
    Serial.begin(115200);
}

void loop()
{
    fsm_process();
}

void fsm_process()
{
  unsigned long tnow = millis();

  switch (curr_state)
  {
    case ST_GREEN:
        digitalWrite(L_Y, 1);
        digitalWrite(L_Y, 0);
        digitalWrite(L_R, 0);

        if (tnow - tbefore >= green_interval || digitalRead(BUT) == 0) {
          curr_state = ST_YELLOW;
          tbefore = tnow;
          Serial.println("Changed to YELLOW!");
        }
        break;

    case ST_YELLOW:
        digitalWrite(L_G, 0);
        digitalWrite(L_Y, 1);
        digitalWrite(L_R, 0);

        if (tnow - tbefore >= yellow_interval) {
          curr_state = ST_RED;
          tbefore = tnow;
          Serial.println("Changed to RED!");
        }
        break;

    case ST_RED:
        digitalWrite(L_G, 0);
        digitalWrite(L_Y, 0);
        digitalWrite(L_R, 1);

        if (tnow - tbefore >= red_interval) {
          curr_state = ST_GREEN;
          tbefore = tnow;
          Serial.println("Changed to GREEN!");
        }
        break;
    default: // Green
        digitalWrite(L_Y, 1);
        digitalWrite(L_Y, 0);
        digitalWrite(L_R, 0);

        if (tnow - tbefore >= green_interval || digitalRead(BUT) == 1) {
          curr_state = ST_YELLOW;
          tbefore = tnow;
          Serial.println("Changed to YELLOW!");
        }
        break;
  }
}
```
### Example # 2

Let's read a DTH11 sensor, available in the kit provided in the laboratory. Lets implement this FSM (**remember to include DHT11 library, as we saw in the last session**):

![fsm_dht11](img/fsm_dht11.png)

The code should be similar to this one:

```Arduino
#include <Arduino.h>
#include "DHT.h"

// --- Pines ---
#define DHTPIN  4        // DHT11 pin
#define DHTTYPE DHT11
#define FAN_PIN  26      // Fan (ej. relay or transistor)
#define ALERT_PIN 27    // Alarm (LED or buzzer)

// --- DHT config ---
DHT dht(DHTPIN, DHTTYPE);

// --- FSM STATES ---
#define NORMAL_MODE   0
#define FAN_MODE      1
#define ALERT_MODE    2
int curr_state = NORMAL_MODE;

// --- Variables de tiempo ---
unsigned long tbefore = 0;
const unsigned long read_interval = 2000; // Read every 2 seconds

void fsm_process();

void setup()
{
  Serial.begin(115200);
  dht.begin();

  pinMode(FAN_PIN, OUTPUT);
  pinMode(ALERT_PIN, OUTPUT);

  digitalWrite(FAN_PIN, LOW);
  digitalWrite(ALERT_PIN, LOW);

  Serial.println("FSM control with DHT11 starting...");
}

void loop()
{
  fsm_process();
}

void fsm_process()
{
    unsigned long tnow = millis();

  // Read every 2 seconds
  if (tnow - tbefore >= read_interval) {
    tbefore = tnow;

    float t = dht.readTemperature();
    float h = dht.readHumidity();

    if (isnan(t) || isnan(h)) {
      Serial.println("Error reading DHT11 sensor");
      return;
    }

    Serial.print("Temp: ");
    Serial.print(t);
    Serial.print(" °C  Humidity: ");
    Serial.print(h);
    Serial.println(" %");

    // FSM: State transtions
    switch (curr_state) {
      case NORMAL_MODE:
        digitalWrite(FAN_PIN, LOW);
        digitalWrite(ALERT_PIN, LOW);

        if (t > 28 && t <= 32) {
          curr_state = FAN_MODE;
          Serial.println(">> Transition to FAN mode");
        } else if (t > 32) {
          curr_state = ALERT_MODE;
          Serial.println(">> Transition to ALERT mode");
        }
        break;

      case FAN_MODE:
        digitalWrite(FAN_PIN, HIGH);
        digitalWrite(ALERT_PIN, LOW);

        if (t <= 28) {
          curr_state = NORMAL_MODE;
          Serial.println(">> Transition to NORMAL mode");
        } else if (t > 32) {
          curr_state = ALERT_MODE;
          Serial.println(">> Transition to ALERT mode");
        }
        break;

      case ALERT_MODE:
        digitalWrite(FAN_PIN, HIGH);
        digitalWrite(ALERT_PIN, HIGH);

        if (t <= 28) {
          curr_state = NORMAL_MODE;
          Serial.println(">> Transition to NORMAL mode");
        } else if (t > 28 && t <= 32) {
          curr_state = FAN_MODE;
          Serial.println(">> Transition to FAN mode");
        }
        break;
    }
  }
}
```

## Embedded Operating System

An *Embedded Operating System (EOS)* is a piece of firmware useful to manage multiple tasks inside a microcontroller. Some of the most used EOS's are: Embedded linux, Free Real-Time OS, TinyOS, ThreadX and mbedOS.

We are going to explore a little bit of FreeRTOS, because is free, open and has been ported to a lot of plattforms (ESP32 included).

## Main References

1. Lesson 2 **A deeper dive into IoT** ([link](https://github.com/microsoft/IoT-For-Beginners/blob/main/1-getting-started/lessons/2-deeper-dive/README.md)) from Microsoft’s **IoT for Beginners** course [[link](https://github.com/microsoft/IoT-For-Beginners)]
2. Lesson 3 **Interact with the physical world** ([link](https://github.com/microsoft/IoT-For-Beginners/blob/main/1-getting-started/lessons/3-sensors-and-actuators/README.md)) from Microsoft’s **IoT for Beginners** ([link](https://github.com/microsoft/IoT-For-Beginners)) by Microsoft.