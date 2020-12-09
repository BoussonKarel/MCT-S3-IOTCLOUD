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
- Vanuit App direct communiceren met MQTT broker via internet.
- Voor meeste platformen (iOS, Android, Windows is dit mogelijk)
- Niet altijd beste oplossing (poorten niet altijd open)

### Bericht via Azure Functions naar MQTT (one way)
![Directe communicatie](https://i.imgur.com/M8YS1gP.png)
- Vanuit App HTTP POST naar Azure Functions
- In de Azure Function maken we bericht aan om te versturen naar MQTT Broker Topic

### Communicatie tussen devices via cloud
![Directe communicatie](https://i.imgur.com/7Mv8NaH.png)
Als we op knop drukken:
- Publish bericht in /howest/gkg/b008/#
- Broker draait in Cloud
- Iedereen met subscription op /howest/gkg/b008/# zal dit ontvangen

### Communicatie tussen devices lokaal zonder cloud
![Directe communicatie](https://i.imgur.com/imFEWa6.png)
- We kunnen een MQTT Broker installeren op de Raspberry Pi
- Devices communiceren met elkaar via de lokale broker op de Pi
- Geen link met de cloud nodig

## Communicatie tussen devices lokaal via gateway met cloud link
![Directe communicatie](https://i.imgur.com/heTfYBJ.png)
- We kunnen een MQTT Broker installeren op de Raspberry Pi
- Devices communiceren met elkaar via de lokale broker op de Pi
- Via een mobile app sturen we bericht naar Azure Function LED AAN
- Function plaatst bericht in Topic /howest/gkg/b008/#
- Vraagt VPN (complex)

## Belangrijk
- Wat is MQTT ?
- Wat zijn topics & subscriptions?
- Welke vormen van topics zijn er , cfr. Wilcardsetc
- Wat is QoSen welke zijn er ?
- Welke opstellingen zijn er mogelijk ?
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwOTAyNzE1NDIsMTc3MzYyNjg4MCwtMT
czNTcyNTE2NSwxNTk2NTc4NTcyXX0=
-->