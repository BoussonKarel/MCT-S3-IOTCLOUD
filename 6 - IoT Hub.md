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
- D2C: Low powered device zal communiceren met Raspi.
- Gateway zal data doorsturen naar Cloud
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYxOTQ0NDQ1NSwxNjU3NjUwNDIzLDg0OT
A4NjIyOSwyMDMxMzkxMzE1LC0xMjkwNDk5MzkyLDE1NTU0ODc5
ODUsLTEyMzEwOTI2NzNdfQ==
-->