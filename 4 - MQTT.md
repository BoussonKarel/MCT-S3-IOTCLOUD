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

**Wildcards**
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
: Resent until sender gets ack.
: Duplicates can occur.

Level 2: Delivered exactly once
: Receiver gets it exactly once.
: More overhead.

---
- **Payload**
  - JSON
  - XML
  - CSV
  - ...
- Geen standaard
- Nadeel is interoperatibility
  - *Samenwerken met andere systemen is moeilijk: geen afspraken rond inhoud.*
  - Goede documentatie nodig.
---
- **Security**
  - Login / wachtwoord
    - Eenvoudig, maar niet veilig (vermijden)
  - TLS (zie 3MCT)
    - Meest veilige
    - Beveiligen van het communicatiekanaal
    - Krachtiger IoT device nodig voor encryptie (niet overal mogelijk)

## Opstellingen
### Directe communicatie (one way)
![Directe communicatie](https://i.imgur.com/DE7HY5V.png)

### Bericht via Azure Functions naar MQTT (one way)
![Directe communicatie](https://i.imgur.com/DE7HY5V.png)

### Communic
![Directe communicatie](https://i.imgur.com/DE7HY5V.png)

### Directe communicatie (one way)
![Directe communicatie](https://i.imgur.com/DE7HY5V.png)

## Belangrijk
- Wat is MQTT ?
- Wat zijn topics & subscriptions?
- Welke vormen van topics zijn er , cfr. Wilcardsetc
- Wat is QoSen welke zijn er ?
- Welke opstellingen zijn er mogelijk ?
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzY5ODc4MTc5LDE3NzM2MjY4ODAsLTE3Mz
U3MjUxNjUsMTU5NjU3ODU3Ml19
-->