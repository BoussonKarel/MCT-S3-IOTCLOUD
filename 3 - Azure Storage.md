# 3 - Azure Storage
- Opslag van data in Cloud omgeving
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
- Hard Disk maar in de Cloud
- Je kan deze mappen naar eigen pc *(bv. Z:\\)*
- Handig: veilig files kopiëren Cloud <> On Premise
- Zal gekende protocollen volgen zoals SMB3.0
- Veel gebruikt in Hybrid Cloud

![Azure Files](https://i.imgur.com/w5SdQjl.png)

## Azure Disk Storage
- Basis voor Azure VM
- Op deze locaties komt de server te staan
- Mogelijk om datadisks te maken
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

+ Bestanden uploaden via Storage Explorer

- Connecteren
  - Account Name/Key

+ Bestanden opvragen via HTTP Request

- Pricing
  - Per GB/Per maand
  - Hot / Cold
  - Lees- en schrijfoperaties

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
  - Zender & ontvanger werken onafhankelijk
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
  - # kolommen per rij moet niet hetzelfde zijn
- Geen relaties, joins, stored procedures
- Eenvoudig in gebruik

![Azure Table Storage](https://i.imgur.com/F8F6m2T.png)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NDA4OTkwMDUsMTMwMTM0NTA4OSw0MD
QzNzk3ODQsLTE3NDE4ODc5OTFdfQ==
-->