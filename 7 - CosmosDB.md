# 7 - CosmosDB
## Wat zijn relationele databases?
- Opslag van data op gestructureerde manier

+ In verschillende tabellen
  + Normalisatie
  + Schema waarin data moet passen

- Tabel
  - Rijen (records) (de data)
  - Kolommen (welke info)

+ Tabellen met elkaar verbinden via relaties
  + Vreemde sleutels (kolom die zal verwijzen naar record in andere tabel)

- We maken gebruik van SQL voor opvragen, toevoegen, wijzigen, verwijderen van data...

+ Via DDL kunnen we tabellen aanmaken...
 
![enter image description here](https://i.imgur.com/l5xD0v6.png)

- Ontslaan in client / server periode
- Nog geen sprake van Internet, Cloud, Mobile data etc...
- Was vooral gemaakt om op 1 server te werken, meestal centraal in bedrijf
- Enige manier om te schalen was krachtig CPU/Network/storage --> Scale up
- Opgepast: blijft zeer belangrijk binnen bedrijven, veel software moet integreren met bestaande systemen waaronder SQL

## Waarom nu plots NoSQL Databases
- Hoeveelheid data neemt enorm toe *(social networks, IoT devices, AI & Deep learning systemen)*
- Concurrency (veel gebruikers op hetzelfde moment)
- Globaal bereikbaar en responsive
- Connectivity (veel gebruikers schrijven of lezen data)
- Verschillende soorten data (structured, semi-structured of unstructured)
- Horizontal scaling (eenvoudig meerdere servers)

^^ Niet altijd mogelijk met relationele databases

### Scaling
- Met eenvoudige hardware (mag goedkoop) scale-out (servers bijplaatsen)
- Geen downtime
- Eenvoudig te installeren en configureren

![](https://i.imgur.com/zQgfovY.png)

### Availibility & always-on
- **RDBMS**
  - 
- **NoSQL**
  - Data op verschillende partities
  - Geen gedeelde data
  - Data naar alle storage, high availibility (complexer met RDBMS)
  - We spreken over nodes

| RDBMS | NoSQL |
|--|--|
| Gedeelde storage failure > Volledige applicatie down | Data op verschillende partities |
| | Geen gedeelde data |
| | Data naar alle storage, high availibility (complexer met RDBMS) |
| | We spreken over nodes |
| ![](https://i.imgur.com/rKURZPi.png) | ![](https://i.imgur.com/0WvIcKI.png) |

### Global Deployment
- Database in verschillende datacenters
- Zo dicht mogelijk bij de klant laten draaien (latency--)
- Automatische replicatie van data tussen verschillende datacenters

### Gedistribueerde systemen
- NoSQL is een gedistribueerd systeem
- Meerdere servers (of nodes)
- Nodes communiceren met elkaar over een netwerk
- Data op meerdere machines (niet merkbaar)

## Soorten NoSQL Databases
1. Key/value
2. Document database
3. Column store
4. Graph

### Key-Value
Table Storage
- Meest eenvoudige noSQL database
- Bestaat uit key (uniek) + één waarde (JSON of ander document)
- Geen datatype (NoSQL weet niet welk soort, slaat enkel op)
- Applicatie moet waarde kunnen interpreteren

+ Waar gebruiken?
  + Sessie informatie gebruiker, user profiles, shopping basket
  + Data waar je minder moet in gaan zoeken via een query
  + Data zonder relaties

### Document databases
- Basis is een **document**, geen record
- Formaat is meestal **JSON**, XML of BSON (binary json) ook mogelijk
- Document zal **zichzelf beschrijven**, geen schema nodig
- Niet ieder document moet volgens hetzelfde schema
- Query taal om data op te vragen en doorzoeken

+ Waar gebruiken?
  + Real-time analytics data
  + IoT applications
  + Data die niet zoveel zal wijzigen *(maar tegenwoordig meer en meer voor alle soorten)*

### Column Store
Data opslag niet op basis van records, maar op basis van kolommen

![](https://i.imgur.com/AXqLpOK.png)

Sneller bij complexe queries
Veel gebruikt voor data analyse systemen

### Graph Database
- Opslaan van entiteit en relaties tussen verschillende entiteiten
- Een entiteit is een soort node (object instantie) met properties
- Relatie bevat ook properties *(bv. friend relation, project relation)*
- Kracht zit in de relaties tussen entiteiten

![](https://i.imgur.com/XGSyJkM.png)

+ Waar gebruiken?
  + Real-time analytics data
  + IoT applications
  + Data die niet zoveel zal wijzigen *(maar tegenwoordig meer en meer voor alle soorten)*

## Voorbeeld NoSQL
- Record zal een document worden
- Makkelijk nieuwe velden toepassen
- Formaat is JSON
- Slaan data op als JSON in database zelf
- Moeten data niet meer uitlezen en INSERT opbouwen

![](https://i.imgur.com/3ZqyFjH.png)

**Nadeel:** dubbele data, geen relaties

## CosmosDB
- CosmosDB is managed database service op Azure
  - Geen onderhoud, patching
  - Eenvoudig op te zetten
  - Pay what you use
  - Krachtige API's
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM2Mjk3NjQwOSwtMjA0OTEzODM2N119
-->