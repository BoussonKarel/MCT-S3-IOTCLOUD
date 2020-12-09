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
  - Krachtig genoeg om veilig 
<!--stackedit_data:
eyJoaXN0b3J5IjpbODQ5MDg2MjI5LDIwMzEzOTEzMTUsLTEyOT
A0OTkzOTIsMTU1NTQ4Nzk4NSwtMTIzMTA5MjY3M119
-->