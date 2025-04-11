# Protocolo One Wire

El protocolo 1-Wire es un sistema de comunicación serial que permite la transferencia de datos y energía entre dispositivos utilizando solo un cable de datos y tierra. Es ampliamente utilizado en sensores de temperatura como el DS18B20 y otros dispositivos de identificación y almacenamiento.

## Conceptos básicos del protocolo 1-Wire

* Un solo cable: Se usa un único hilo para la comunicación y, en algunos casos, también para la alimentación.

* Direcciones únicas: Cada dispositivo tiene un identificador de 64 bits único.

* Modo de alimentación parasitaria: Algunos dispositivos pueden operar sin una fuente de alimentación dedicada.

* Comunicación maestro-esclavo: Un controlador (maestro) se comunica con múltiples dispositivos (esclavos).

## Principio de funcionamiento de la comunicación
* Reset y presencia: El maestro envía un pulso de reinicio y espera una respuesta de los dispositivos conectados.

* Comandos ROM: Se utilizan para identificar y seleccionar dispositivos específicos.

* Lectura y escritura de datos: Se transmiten bits mediante tiempos específicos de señal.

## Ejemplo de uso con Arduino

Se muestra un ejemplo con un sensor de temperatura DS18B20 en Arduino IDE, normalmente se emplea la librería OneWire:

```ino
#include <OneWire.h>
#include <DallasTemperature.h>

#define PIN_SENSOR 2  // Pin donde está conectado el DS18B20

OneWire oneWire(PIN_SENSOR);
DallasTemperature sensors(&oneWire);

void setup() {
    Serial.begin(9600);
    sensors.begin();
}

void loop() {
    sensors.requestTemperatures(); // Solicitar la lectura de temperatura
    float tempC = sensors.getTempCByIndex(0); // Obtener la temperatura en grados Celsius
    Serial.print("Temperatura: ");
    Serial.print(tempC);
    Serial.println(" °C");
    delay(1000); // Esperar un segundo antes de la siguiente lectura
}
```

## Otros ejemplos

1. Ejemplo 1 [[link]](dht11/esp32/README.md)


## Referencias

1. https://blog.mbedded.ninja/electronics/communication-protocols/1-wire-protocol/
2. https://docs.onion.io/omega2-docs/communicating-with-1w-devices.html
3. https://docs.arduino.cc/learn/communication/one-wire/
4. https://www.analog.com/en/resources/technical-articles/using-a-uart-to-implement-a-1wire-bus-master.html
5. https://onlinedocs.microchip.com/pr/GUID-1618003F-992B-4E48-9411-5E5D5D952C06-en-US-3/index.html?GUID-EE2B21FC-9AA9-4C04-88EF-1951F703A56C
6. https://www.analog.com/en/resources/technical-articles/guide-to-1wire-communication.html
7. https://www.mikrocontroller.net/attachment/239139/One-Wire-Bussysteme.pdf
8. https://web.fdi.ucm.es/posgrado/conferencias/MariaEmiliaCambronero2017-slides.pdf
9. https://ww1.microchip.com/downloads/aemDocuments/documents/OTH/ApplicationNotes/ApplicationNotes/01199a.pdf
10. https://en.wikipedia.org/wiki/1-Wire
11. https://pdfserv.maximintegrated.com/en/an/AN148.pdf
12. https://www.cs.unb.ca/tech-reports/documents/TR15-235.pdf
13. https://opencircuits.com/images/a/a3/A_Guide_to_the_1WRJ45_Standard.pdf
14. https://www.unipi.technology/shop/product/download?fileId=142
15. https://resources.altium.com/es/p/comparing-all-serial-communications-protocols
16. https://learn.sparkfun.com/tutorials/serial-communication/all
17. https://www.hackster.io/ubidots/projects
18. https://www.hackster.io/projects
19. https://www.hackster.io/chipmc/smart-and-safe-outdoor-plant-watering-system-new-for-2018-17d5c8
20. https://www.hackster.io/clementchamayou/how-to-monitor-a-beehive-with-arduino-nano-33ble-bluetooth-eabc0d
21. https://hackaday.io
22. https://ubidots.com/blog/tag/iot-projects/
23. https://learn.adafruit.com/digikey-iot-studio-smart-home/overview
24. https://www.digikey.com/en/maker
25. https://www.seeedstudio.com/blog/2021/02/02/fun-esp32-projects-you-need-to-try/
26. https://www.electrondust.com/2018/11/11/esp-32-micro-robot-arm/
27. https://lab.bricogeek.com/proyecto/mini-robot-tanque-con-esp32/materiales
28. https://randomnerdtutorials.com/esp32-cam-car-robot-web-server/
29. https://www.ti.com/document-viewer/ja-jp/lit/html/SSZT164
30. https://www.hackster.io/MisterBotBreak/how-to-use-a-big-sound-sensor-657ec6
31. https://www.robotique.tech/robotics/obstacle-detection-system-with-esp32/
