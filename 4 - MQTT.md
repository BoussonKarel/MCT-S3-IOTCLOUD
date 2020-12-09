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
Sectoren: *Telemetry, Automotive, Smart Home, Energy Monitoring, Chat Apps, Notification Services, Healthcare Apps, LoRa Gateway, Facebook Messenger, Olie & Gas*

---
- Broker (server) heeft een **topic** of **subject**
- Zelfde vorm as URL
+ Devices hebben subscription op één of meerdere topics

![Topic](https://i.imgur.com/TRvBZAL.png)

![Wildcards](https://i.imgur.com/baiMU6E.png)

![Wildcards](https://i.imgur.com/TByshhT.png)

---
- **QoS** (Quality of Service)
- 3 niveau's

Level 0: Fire And Forget
: Relies on reliability of TCP.
: No retransmission.

Level 1: Delivered at least once
: Receiver will get it at least once.
: No ack (or it gets lost) --> Resent until s
: Duplicates can occur.

Level 2: Delivered exactly once
: Relies on reliability of TCP. No retransmission.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExODY5MDI2NDMsLTE3MzU3MjUxNjUsMT
U5NjU3ODU3Ml19
-->