# 2 - Backend Services met Azure Functions
## The Internet of ??
- Webpagina's met content
  - Opzoeken van informatie
  - Raadplegen van informatie
  - E-commerce
  - Social networks
- ...
- Technologie: HTML, CSS, JS, PHP / ASP / JAVA
![The Internet of ??](https://i.imgur.com/9C0b2Vj.png)

## The Internet of Services
- Connectiviteit
  - Driving factor mobile apps
  - Cross platform
  - Data op makkelijke manier uitwissen
  - Functionaliteit makkelijk aanroepen
  - Centraal staan Cloud platforms
  - REST Based
![The Internet of Services](https://i.imgur.com/462lUmV.png)

## The Internet of Things
- Connecting hardware
  - Device koppelen aan internet
    - Informatie versturen naar Cloud
    - Toestellen onder elkaar (Machine 2 Machine)
  - Communicatie van/naar toestel
    - Berichten naar toestel (verzenden)
    - Berichten van toestel (ontvangen)

![The Internet of Things](https://i.imgur.com/GU8ljua.png)

## Wat is de volgende stap?
### The Internet of Value
- **Value** verhandelen via het internet
  - Bitcoin
  - Cryptocurrencies

+ Onderliggende technologie veel belangrijker
  + Blockchain
    + Distributed ledger (grootboek)
    + Registreren transacties
    + Elke transactie: verwijzing naar vorige transacties (chain)

- Blockchain (public, gratis, open)

+ Private blockchain mogelijk
  + Veel evolutie in de wereld van fintech
  + Etherium
  + Smart Contracts

## Hoe werkt HTTP?
### HTTP
OSI: *Application Layer*

**H**yper**T**ext **T**ransfer **P**rotocol
- Onderliggende protocol waarop Internet werkt
- Opvragen van tekst, bestanden vanaf servers
- Request meestal afkomstig v/e webbrowser, maar ook smartphone, IoT device
- HTTP zal bepalen hoe een request en response er moeten uitzien
- HTTP bevat een aantal commando's (HTTP verbs)
- HTTP is stateless, houdt geen rekening met voorgaande requests
- HTTP is niet sessionless, we kunnen cookies gebruiken om data bij te houden
- HTTP is relatief eenvoudig

#### HTTP Verbs
| Verb | |
|--|--|
| **GET** | Ophalen data (safe, wijzigt niks) (**SELECT**) |
| **POST** | Toevoegen data (**INSERT**) |
| **PUT** | Idempotent > Meerdere requests > Zelfde effect (**UPDATE**) |
| **DELETE** | Idempotent > Meerdere requests > Zelfde effect (**DELETE**) |

#### HTTP Status codes
| Status code| Betekenis |
|--|--|
| **1xx** | Informatief |
| **2xx** | Succes |
| **3xx** | Redirection |
| **4xx** | Client error |
| **5xx** | Server error |

### HTTPS
- Beveiligen van transport
- Geen beveiliging van de data
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

## HTTP/2
- Sinds 2015 actief
- High-level compatibility with HTTP/1.1
  - Methods, status codes, URIs and header fields.
- Request multiplexing over a single TCP connection
  - Meerdere requests in parallel mogelijk over 1 tcpconnection
  - Asychroondownloadenvan meerderebestandenmogelijk
- Header Compression
- BinaryProtocol (HTTP/1.1 is tekst protocol)
- HTTP/2 Server push

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NzEzNTYwMjksLTE4ODQxNjA2NzQsMT
k2NTI3ODE4LC0yMTI5OTE0MDldfQ==
-->