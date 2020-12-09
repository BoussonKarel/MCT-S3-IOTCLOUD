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

## Azure Files
- Hard Disk maar in de Cloud
- Je kan deze mappen naar eigen pc *(bv. Z:\\)*
- Handig: veilig files kopiëren Cloud <> On Premise
- Zal gekende protocollen volgen zoals SMB3.0
- Veel gebruikt in Hybrid Cloud

## Azure Disk Storage
- Basis voor Azure VM
- Op deze locaties komt de server te staan
- Mogelijk om datadisks te maken
- Hoge beschikbaarheid
- Lage latency
- Hoge troughput (2000MB/s)
- Mogelijkheid voor SSD disk
- Disk Encryption beschikbaar

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

Cool Acc
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYyNDM0NDE3NSwxMzAxMzQ1MDg5LDQwND
M3OTc4NCwtMTc0MTg4Nzk5MV19
-->