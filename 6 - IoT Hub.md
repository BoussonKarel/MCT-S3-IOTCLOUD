# 6 - IoT Hub
## Wat is IoT Hub?
Azure IoT Hub is a fully managed service that enables **reliable** and secure **bidirectional communications** between **millions** of IoT devices and a **solution back end**

- Managed Service
- Bi-Directional Communication
- Miljoenen toestellen
- Support voor meerdere talen (C#, Python, C, Node)
- HTTPS/AMQP/MQTT protocol support
- Versturen telemetrie data: Device to Cloud
- Ontvangen van commands: Cloud to Device
- Beheer van devices via digital twin
- Queries op devices
---
- End-to-end security
- Certificaten per device
- TLS support
- X,509 support
- IP whitelisting / blacklisting van devices
- Firmware / software update support
- Eenvoudiger dan bij MQTT
---
- Device zal rechtstreeks communiceren met IoT Hub
  - Device To Cloud (D2C)
  - Cloud To Device (C2D)
- Drie protocollen mogelijk
  - AMQP
  - MQTT
  - HTTPS
- Meest eenvoudige opstelling
- Hardware moet wel krachtig genoeg zijn
  - Raspi, Sparkfun
---
Device zit rechtstreeks op het internet
![Device zit rechtstreeks op de hub](https://i.imgur.com/YAc8Pv8.png)

---
- Wat als device niet krachtig genoeg is?
  - Arduino, Mbed Cortex M0, M1...
  - Goedkope hardware (kan niet altijd connecteren op internet)
- Oplossing
  - Field gateway *(RPi, Industriële PC)*
  - Krachtig genoeg om veilig met internet te communiceren
  - Field gateway zal lokaal met minder krachtige device praten via CoAP, Bluetooth AllJoyn...

![Field Gateway](https://i.imgur.com/sqMdoWf.png)

---
![D2C / C2D](https://i.imgur.com/3RQXsex.png)
- D2C: Low powered device zal communiceren met Raspi (Gateway).
  - *Gateway zal data doorsturen naar Cloud*
- C2D: IoT Hub zal commando sturen naar Raspi (Gateway)
  - *Raspi zal commando naar juiste device sturen*
---
Hoe data verwerken die binnenkomt op IoTHub
- Streaming Analytics
- Message Queues
- Azure Functions
  - Ontvangen van berichten
  - Versturen van berichten (commando) naar IoT Hub

![D2C & C2D](https://i.imgur.com/8TP56YF.png)

### IoT Hub Device Twin
- Digitale "tweeling" van device cloud
- Ideaal om **configuratie** naar een toestel te sturen
- Configuratie zal opgeslagen
  - In de Cloud (IoT Hub)
  - Op het toestel *(bv. variable in Python)*
- Alles wat configureerbaar moet zijn op afstand
- *Bv. Threshold voor temperatuur meter*

+ **Reporting properties**
  + Device kan rapporteren aan cloud
  + Batterijstatus
  + Toestelstatus
  + Laatste upload toestel > cloud

- **Device Methodes**
  - Methodes op toestel activeren vanop afstand
  - We gaan de effectieve Python methode vanop afstand starten
  - *Bv. reboot*

- **IoT Hub Device Direct Method**
  - Python methode vanop afstand uitvoeren
  - Via portal, C#
  - Parameters meesturen mogelijk

+ Queries mogelijk op twins

### IoT Hub Trigger for Azure Functions

- Data is Array van bytes
  - Omzetten naar string (json)

## IoT Edge
- **IoT Hub issues**
  - Alles moet naar de cloud voor werking, niets lokaal, veel datatrafiek
  - Afhankelijk van het internet
  - Moeilijk scripts op een device te updaten
  - Script vraagt soms libraries op devices (soms probleem met installatie)
  - Versie beheer lastig
  - Soms wil je bepaalde data NIET naar cloud sturen (binnen bedrijf houden)

**IoT Edge**
: Service boven op IoT Hub
+ Doelstelling:
  + Cloud workloads lokaal draaien
  + Eerste filtering van data op device
  + Niet alles naar Cloud
  + Offline scenario voorzien
  + Kosten in de Cloud dalen
  + Makkelijk updaten van IoT Edge device

- 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MjA3NzM4MjEsLTE4ODMxMDQxMjMsLT
g4NTQ3NjMzNCwzOTk0NTI3NDgsMjA0MjMyNDQ1Nyw5MTkwNTM3
NDEsMTY1NzY1MDQyMyw4NDkwODYyMjksMjAzMTM5MTMxNSwtMT
I5MDQ5OTM5MiwxNTU1NDg3OTg1LC0xMjMxMDkyNjczXX0=
-->