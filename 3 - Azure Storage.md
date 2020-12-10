# 3 - Azure Storage
- Zeer flexibel in gebruik en prijs
- Unlimited storage *(limiet ligt hoog)*
- Basis voor heel wat Azure Services
  - VM's, Functions...

Vijf soorten storage
: (File)
: (Disk)
: Blob
: Queue
: Table

Alles komt samen onder een **Azure Storage Account**, hierbinnen maak je de soorten storage aan.

![Azure Storage Account](https://i.imgur.com/c4F4KtA.png)

## Azure Files
- Hard Disk in de Cloud
- Mappen mogelijk *(bv. Z:\\)*
- Veilig files kopiëren Cloud <> On Premise
- Zal gekende protocollen volgen zoals SMB3.0
- Veel gebruikt in Hybrid Cloud

![Azure Files](https://i.imgur.com/w5SdQjl.png)

## Azure Disk Storage
- Basis voor Azure VM
- Op deze locaties komt de server te staan
- Datadisks maken mogelijk
- Hoge beschikbaarheid
- Lage latency
- Hoge troughput (2000MB/s)
- Mogelijkheid voor SSD disk
- Disk Encryption beschikbaar

![Azure Disk Storage](https://i.imgur.com/fD041jI.png)

## Azure Blob Storage
- Opslag van bestanden
  - *Afbeeldingen, PDF, CSS, JS files van web apps kan je hier plaatsen*
- Single page apps (Vue, Angular, Blazor)
- Container
  - Bevat de bestanden
  - Naam opgeven
  - Public Access Level (wie kan welke bestanden zien)
    - Private (default) extern bekijken is niet mogelijk
    - Blob (extern lezen per blob is mogelijk)
    - Container (extern lezen van volledige container is mogelijk)
---
Bestanden uploaden via Storage Explorer

---
Pricing
: Per GB/Per maand
: Hot / Cold
: Lees- en schrijfoperaties

---
Hot Access
: Data die nu in gebruik is en waar we veel lezen en schrijven
: Data die klaar staat om eventueel later naar cool storage te verplaatsen

Cool Access
: Backup voor lange termijn
: Data die we niet frequent nodig hebben

Static Website
: Eenvoudige HTML site
: Ideaal voor VueJS, Angular, Reactor, Blazor...
: Eventueel backend in Azure Functions (via JS aanroepen)
: Zeer goedkoop

## Azure Storage Queues
- Een **wachtrij** in de Cloud
- Applicatie zal berichten op wachtrij plaatsen (**Sender**)
- Tweede applicatie kan deze op zelf gekozen moment ophalen en verwerken (**Receiver**)
- We spreken over een **decoupled** applicatie
  - Zender & ontvanger werken **onafhankelijk**
- Zeer schaalbaar door meerder queues op te starten
- **Resilience**: buffer van berichten op queue zorgt ervoor dat er niets verloren gaat als back-end wegvalt.

*Voorbeeld: Webshop*
![Voorbeeld Queues: webshop](https://i.imgur.com/8ksoWv7.png)

- **Load Leveling**
  - Constante load op applicatie die verwerkt moet worden
  - Werkt zolang we niet meer berichten aanmaken dan wat de applicatie kan verwerken

![Load Leveling](https://i.imgur.com/U5CmrN1.png)

- **Load Balancing**
  - Teveel berichten per uur
    - Applicatie die verwerkt scalen
    - Nieuwe instantie => verdubbeling verwerking
  - Wanneer terug minder => 1 applicatie stoppen
  - High availibility => Als 1 app crasht, ligt het niet plat

![Load Balancing](https://i.imgur.com/CkqPmXP.png)

- **Temporal Decoupling**
  - Alles in de Queue voor later
  - Applicatie start om 23u op
    - Verwerkt alles
    - Shutdown app

![Temporal Decoupling](https://i.imgur.com/S5jFOQn.png)

## Azure Table Storage
- NoSQL key:value store
- Opslag van peta bytes aan data
- Geo-redundant storage
- Flexibel dataschema
  - \# kolommen per rij moet niet hetzelfde zijn
- Geen relaties, joins, stored procedures
- Eenvoudig in gebruik

![Azure Table Storage](https://i.imgur.com/F8F6m2T.png)

### Partitions
Verdelen van table over partities
  - Iedere partitie op eigen server
  - Zal beter schalen en load verdelen over server
- Load balancing over 3 server
  - Azure zal data repliceren op 3 servers
  - Verdelen van load over deze servers

![Partitioning Tables](https://i.imgur.com/xvssTLF.png)

---
- Entities (rij)
  - Max 1MB
  - 255 properties (kolommen)
    - 3 verplicht
      - Partition Key
      - Row Key
      - Timestamp *(automatisch)*
    - Niet iedere rij moet evenveel kolommen hebben
---
+ Table Storage Data Access
  + REST API
    + Cross platform HTTP Requests (.NET, PHP, Android, Objective C...)
  + Storage Client API (via NUGET Package Azure Storage)
  + Andere platformen zijn er ook libraries
    + iOS, Android, Python...
---
- Queries
  - Max. 1000 items terugkeren
  - Indien > 1000
    - Continuation token
  - Query > 30 sec = cancelled
  - Geen index mogelijk
  - Query op partition & row key = snel
---
+ Kolom types
  + Byte[]
  + Bool
  + DateTime
  + Double
  + Guid
  + Int32 or int
  + Int64 or long
  + String
---
**Waar zouden we dit kunnen gebruiken ?**
- Profiel info (zal niet veel wijzigen)
- Device info
  - *Bv. alle IMEI nummers van GSM toestellen binnen een netwerk*
- TelemetryData
  - *Bv. sensor netwerken die om de 5 sec waarde van (temperatuur) sensor doorsturen*
- Data voor AI modellen
- Alles waar je zeer veel niet veel wijzigende data wenst op te slaan

## Programmeren van Azure Storage?
- Wanneer?
  - Uploaden van bestanden op Blob Storage
  - Versturen van berichten naar Queues
  - Wegschrijven van records naar table storage
- Allemaal te programmeren via C#, Python of JS

## Enkele Scenario's
### Scenario 1
![Scenario 1](https://i.imgur.com/kCTSurn.png)

### Scenario 2
![Scenario 2](https://i.imgur.com/NRNZFM4.png)

**Blob Trigger**
Functie uitvoeren als er een Blob file aangemaakt is in een container *(bv. uploaden van foto's, csv... naar blob voor verdere verwerking)*

**E-mail versturen** 
Met SendGrid
![SendGrid](https://i.imgur.com/RX7Ftd7.png)

Of MailKit (alternatief, geen mailservice)

### Scenario 3
![Scenario 3](https://i.imgur.com/AFJD5M1.png)

**Queue Trigger**
Bij ontvangst van een bericht op de queue
- Ideaal voor bufferen bij pieken
- Eenvoudig

## Good practices
- Iedere Azure Function heeft eigen taak
  - ~~Eén trigger: *file Upload + mail*~~
  - Meerdere triggers = schaalbaar; hogere performantie
    - HTTP Trigger: *file naar Blob*
    - Blob Trigger: *bericht op queue*
    - Queue Trigger: *mail sturen*

## Wat met configuratie files online
| Offline | Online (via de portal) |
|--|--|
| In 'local.settings.json' | Configuration > Application settings |

## Belangrijk
- Welke zijn de verschillende soorten Azure Storage en wat is hun doel ?
- Wat is Azure Blob storage en wanneer gebruik je deze?
- Wat is Azure Storage Queues en wanneer gebruik ik deze?
- Wat is Azure Table Storage en wanneer gebruik ik deze?
- Wat zijn partitions in Azure Table Storage?
- Hoe werken Azure Functions BlobTriggers?
- Waarvoor kan ik Azure Functions Blob Trigger gebruiken?
- Wat is SendGrid?
- Good practices
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk4OTMwMjksMTYyMTU0NTcyNywxMzgxMj
MzNzI3LC0xOTgwMDkyNTY3LC04MTkyNzYyMTgsODM2MDAwMDYx
LC0yMTMwNDIyMTM1LDEzMDEzNDUwODksNDA0Mzc5Nzg0LC0xNz
QxODg3OTkxXX0=
-->