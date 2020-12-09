# 4 - MQTT
| Pi --> Cloud | Cloud --> Pi |
|--|--|
| Webservice | ?? |
# MQTT
![MQTT werking](https://i.imgur.com/anwfSw4.png)

- Broker staat centraal
- Doet niets anders dan berichten doorsturen en ontvangen

![(Un)managed services](https://i.imgur.com/fAhYOSM.png)

MQTT
: Message Queueing Telemetry Transport
: M2M (machine-to-machine data transfer protocol)

- Doel
  - Data verzamelen op device voor transport naar cloud
  - Data vanuit de cloud naar de device versturen
  - Communicatie tussen machines (M2M)
    - *Bv. tussen Raspberry Pi en ESP32*
- Voordeel
  - Lightweight (weinig overhead)
  - Bi-directioneel
  - Standaard (versie 3.1.1)
  - Eenvoudig in gebruik
---
- We spreken van een Publishing / Subscriber protocol
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjYzOTE1NzI5LDE1OTY1Nzg1NzJdfQ==
-->