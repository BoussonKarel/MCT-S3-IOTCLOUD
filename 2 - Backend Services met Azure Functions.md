# 2 - Backend Services met Azure Functions
## The Internet of ??
- **The Internet of Information**
- Webpagina's met content
  - *Opzoeken / raadplegen van informatie*
  - *E-commerce*
  - *Social networks*
- Technologie: HTML, CSS, JS, PHP / ASP / JAVA

![The Internet of ??](https://i.imgur.com/9C0b2Vj.png)

- **The Internet of Services**
- Connectiviteit
  - *Mobile apps*
  - *Cross platform*
  - *Data gemakkelijk uitwisselen*
  - *Functionaliteit makkelijk aanroepen*
  - *Centraal staan Cloud platforms*
  - *REST Based*

![The Internet of Services](https://i.imgur.com/462lUmV.png)

- **The Internet of Things**
- Connecting hardware
  - Device koppelen aan internet
    - Informatie versturen naar Cloud
    - Toestellen onder elkaar (Machine 2 Machine)
  - Communicatie van/naar toestel
    - Berichten naar toestel (verzenden)
    - Berichten van toestel (ontvangen)

![The Internet of Things](https://i.imgur.com/GU8ljua.png)

## Wat is de volgende stap?
- **The Internet of Value**
- Value verhandelen via het internet
  - *Bitcoin en andere Cryptocurrencies*

+ Onderliggende technologie veel belangrijker
  + Blockchain (public, gratis, open)
    + Distributed ledger (grootboek)
    + Registreren transacties
    + Elke transactie: verwijzing naar vorige transacties (chain)

- Private blockchain mogelijk
  - Veel evolutie in de wereld van fintech
  - Etherium
  - Smart Contracts

## Hoe werkt HTTP?
### HTTP
OSI: *Application Layer*

**H**yper**T**ext **T**ransfer **P**rotocol
- Onderliggende protocol waarop Internet werkt
- Opvragen van tekst, bestanden vanaf servers
- Request meestal afkomstig v/e webbrowser, maar ook smartphone, IoT device
+ HTTP zal bepalen hoe een request en response er moeten uitzien
+ HTTP bevat een aantal commando's **(HTTP verbs**)
+ HTTP is **stateless**, houdt geen rekening met voorgaande requests
+ HTTP is **niet sessionless**, we kunnen cookies gebruiken om data bij te houden
+ HTTP is relatief eenvoudig

### HTTP Verbs
| HTTP Verb | Waarvoor wordt het gebruikt |
|--|--|
| **GET** | Ophalen data (safe, wijzigt niks) (**SELECT**) |
| **POST** | Toevoegen data (**INSERT**) |
| **PUT** | Idempotent > Meerdere requests > Zelfde effect (**UPDATE**) |
| **DELETE** | Idempotent > Meerdere requests > Zelfde effect (**DELETE**) |

### HTTP Status codes
| Status code| Betekenis |
|--|--|
| **1xx** | Informatief |
| **2xx** | Succes |
| **3xx** | Redirection |
| **4xx** | Client error |
| **5xx** | Server error |

### HTTPS
- Beveiligen van transport
- ~~Beveiligen van de data~~
- Defacto standaard: zonder HTTP niet in productie plaatsen.

### HTTP Request
![HTTP Request header](https://i.imgur.com/gnjdSnE.png)
| Belangrijkste header info ||
|--|--|
| GET | HTTP Verb |
| Host | De server |
| User-Agent | Wie doet het request? |
| Acept | Welk type data kan de client ontvangen? |

### HTTP Response
![HTTP Response header](https://i.imgur.com/wlm67pP.png)
| Belangrijkste header info ||
|--|--|
| 200 OK | Status code |
| Content-Type | Type info *(bv. text/html)* |
| Inhoud | *Bv. HTML code* |
![HTTP Response content](https://i.imgur.com/Nh5aFHU.png)

### HTTP/2
- High-level compatibility with HTTP/1.1
  - *Methods, status codes, URIs and header fields*
- Request multiplexing over single TCP connection
  - Meerdere requests parallel over 1 TCP connectie
  - Asynchroon downloaden van meerdere bestanden
- Header Compression
- Binary Protocol (HTTP/1.1 is tekst protocol)
- HTTP/2 Server push

## Wat zijn nu webservices?
**Functies die we kunnen aanroepen via het internet.**
- **Opvragen van data** via het internet
- **Devices aanspreekbaar maken** via het internet
- Protocol is default (HTTP)
- **Technologie onafhankelijk**
  - *Java, C#, PHP, Python*
- **Platform onafhankelijk**
  - *Windows, Linux, Android, iOS...*
- 2 protocollen
  - SOAP
  - REST
- Datatransport via
  - *XML, JSON...*
---
+ Open data
  + Data die vrij beschikbaar is, opvraagbaar via webservices

- Cognitive services
  - AI API op Azure

+ Internet of Things
  + *Philips Hue API, Parrot AR Drone...*

- Maken gebruik van HTTP
- GET/POST Request naar device
- In de body van het request JSON data
- Cross-platform

### JSON
**J**ava**S**cript **O**bject **N**otation
- Eenvoudig + zeer licht
- Alles tussen {}
- key:value
  - Key met quotes
  - (key:value) pairs scheiden met komma

![JSON format](https://i.imgur.com/UQISVsI.png)

Complexe JSON
- Value kan terug een JSON bevatten
- Daarbinnen terug een key met nieuwe JSON string
- Zoveel nesten als je wil

![Complexere JSON: nesten](https://i.imgur.com/CRw5mfX.png)

Complexe JSON Arrays
- Wanneer er meerdere JSON objecten zijn spreken we van een array
- Deze plaatsen we tussen []
- Value kan een array van JSON objecten zijn

![Complexere JSON: list](https://i.imgur.com/DV4AXjg.png)

### URI
Alles uniek identificeerbaar via een URI --> Uniform Resource Locator (URL)
- Gebruik geen spaties in de URL
- Gebruik meervoud voor resource namen
- Geen hoofdletters
- Gebruik geen HTTP Verb om operatie aan te duiden (in URL)

| URL | OK/NOK |
|--|--|
| /api/getUser/1 | **NOK**: operatienaam in URL + hoofdletters|
| /api/users/1 | **OK**: meervoud resource naam + id van user |

### HTTP GET
- Database zal SELECT uitvoeren
- Data is **read only**
- Return status code:
  - 200 OK + body met opgevraagd object

### HTTP POST
- Database zal INSERT uitvoeren
- Data doorsturen **via body** in JSON
- Return status code:
  - 200 OK + body met toegevoegde object

### HTTP PUT
- Database zal UPDATE uitvoeren
- Data doorsturen **via body** in JSON
- Return status code:
  - 200 OK + body met gewijzigde object

### HTTP DELETE
- Database zal DELETE uitvoeren
- Data doorsturen **via body** in JSON
- Return status code:
  - 200 OK + body met verwijderde object
  - 204 OK + No Content

---
- Wat als er iets fout loopt?
  - Wat terugkeren?
  - Internam Server Error 500 + informatie die je zelf opstelt
  - Denk na welke info:
    - Geen connectie info
    - Geen database namen
    - Geen SQL statements
    - Geen exceptions / interne foutmeldingen
    - ...
---
- Webservices zijn **stateless**
  - GEEN state van de client bijhouden aan server kant
  - GEEN sessies gebruiken
  - Bij iedere request alle info meesturen
  - Iedere request is onafhankelijk van elkaar
  - Verhoogt de schaalbaarheid
  - Eenvoudiger applicatiedesign

## Hoe maken we Webservices
- Aanwezig in ieder platform
- PHP
  - Laravel, Lumen, Wave...
- Python
  - Eve, Flask-Restfull
- .NET
  - ASP.NET Core met C#
  - Azure Functions
    - Met C#, NodeJS of Python

## Azure Functions
**Serverless Functions**
- Waarom Azure Functions?
  - Eenvoudig concept
  - Eenvoudig aan te maken
  - Ondersteuning verschillende talen
  - Snel en eenvoudig schaalbaar

### Azure Functions Security
+ Iedereen kan functie aanspreken
  + Geen controle over wie wat doet
  + Hacker kan factuur doen oplopen: constant aanroepen
  + Andere gebruikers: tragere API

- Drie soorten security
  - Anonymous: iedereen
  - Function
  - Admin

+ Function key: *Enkel bij gekozen functie*
+ Admin key: *Alle functies*

- Key zit in de URL

+ ✅ Makkelijk op te zetten
+ ✅ Beheer keys valt mee bij niet veel gebruikers
+ ✅ Ideaal voor scenario met control over de client
  + Interne Android / iOS (app niet publiek)
  + Interne web apps

- ❌ Key moet in applicatie zitten
- ❌ Veel gebruikers: key management

+ Oplossing: Azure Active Directory B2C
+ JWT Tokens
+ Inloggen via Facebook, Twitter, Google, Microsoft...

### Andere Azure Functions
- HTTP Trigger
  - Webservice
+ Timer trigger
  - Via cron expressie de functie op een tijdstip uitvoeren
- IoT Hub Trigger
+ ...

## What's Next
- Welke nieuwe technologieën volgen?
  - GraphQL
    - Query Taal voor API
    - Queries doorsturen naar de API die resultaten zal terugkeren
    - In volle ontwikkeling
  - gRPC
    - Open Source Remote Procedure Framework
    - We roepen methodes aan op remote servers
    - Platform onafhankelijk en open source
    - Enkel HTTP/2

## Azure Functions Aanroepen
### Raspberry Pi
Python: requests library

**GET**
```python
import requests
url = "..."
ret = requests.get(url)
print(ret.status_code)
print(ret.text)
```
> 200
> "Hello again Python"

**POST**
```python
import requests
import json

payload = { 'getal1': 4, 'getal2': 2 }
url = "..."
json = json.dumps(payload)
ret = requests.post(url, data=json)
print(ret.status_code)
print(ret.text)
```
> 200
> {"quotient": 2}

**JSON inladen en opvragen**
```python
jsonstring = ret.text
obj = json.loads(jsonstring)
print("Het resultaat is {}".format(obj["quotient"]))
```

### .NET
HttpClient > Zie **Device Programming**

## Belangrijk
- Over welke soorten “Internet” spreken we ?
- Wat zijn Webservices en hun eigenschappen?
- Wanneer moet je GET POST PUT DELETE gebruiken?
- Welk HTTP verbszijn idempotent?
- Welke statuscodes moet ik terugsturen?
- Wat is JSON en zorg dat je manueel JSON kan schrijven?
- Hoe kan je Azure Functions aanroepen vanuit Python?
- Welk soorten Azure Functions zijn er?
- Wat is een cron expression?
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNzExODUyNTIsOTM1MTAwNTQ5LC0zND
QwMzc1NjcsNzU3MTI2MjA2LDEyOTk3OTcwODIsMzgxODI1MDEx
LDY0NDE2NjM5OSw4NjE2ODYzMTgsMjA3Mjc2MDk0MywtMTQzNj
gzODk5OCwxNDMwOTMxMzk4LC0xODg0MTYwNjc0LDE5NjUyNzgx
OCwtMjEyOTkxNDA5XX0=
-->