# 4 - MQTT
| Pi --> Cloud | Cloud --> Pi |
|--|--|
| Webservice | ?? |
# MQTT
![MQTT werking](https://i.imgur.com/anwfSw4.png)

- Broker doet niets anders dan berichten doorsturen en ontvangen

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
- We spreken van een **Pub**lishing / **Sub**scriber protocol
- Centraal staat de broker die bemiddeling doet tussen clients
- Eén of meerdere client subscriben op een **topic**
- Eén of meerdere client kunnen een bericht plaatsen op een **topic**
- Pub/Sub weten niets van elkaars bestaan af (geen IP, ports, locatie...)
- Pub/Sub moeten niet op hetzelfde moment actief zijn, kan **disconnected** werken
---
Mogelijke MQTT brokers: *mosquitto, HiveMQ, Apache ActiveMQ, RabbitMQ, mosca, RSMB, WebsphereMQ / IBM MQ*
---

<!--stackedit_data:
eyJoaXN0b3J5IjpbNjE3ODgzNDk1LDE1OTY1Nzg1NzJdfQ==
-->