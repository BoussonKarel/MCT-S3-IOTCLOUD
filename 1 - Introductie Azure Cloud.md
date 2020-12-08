# 1 - Intro Azure Cloud
## Wat is Cloud Computing
### Enkele eigenschappen
- Geen eigen hardware
- Unlimited computing power
- Unlimited storage capacity
- Scaling up and down (op aanvraag / automatisch)
- Scaling in and out (op aanvraag / automatisch)
- Geografische spreiding
- Pay what you use

![Van On premise tot SaaS](https://i.imgur.com/Ne9mMxp.png)

### On Premise (eigen servers)
- IT afdeling **verantwoordelijk voor ALLES**
  - Back-up + recovery
  - Aankoop hardware
  - Scaling
- **Investeren in hardware** die je beperkt nodig hebt (*bv. kerst*)
- Meeste **vrijheid**
- Soms **verplicht door wetgeving**
  - Medische data
  - Financiële data
- Gebrek aan **vertrouwen** public cloud provider

### Hybrid (On Premise & Cloud)
- Eigen datacenter koppelen aan cloud omgeving
- **Bepaalde diensten in cloud**, andere in eigen datacenter
- Zware load uitvoeren op de cloud
- Bepaalde data **verplicht** On Premise (*medical...*)
- Back-up scenario's

### IaaS (Infrastructure as a Service)
- Geen eigen hardware
- **Virtual Machines** in Cloud omgeving
- **Verantwoordelijkheid:**
  - Configureren
  - Beveiligen
  - Updaten
- **Vrijheid:** software
- Zelf scaling doen (soms auto)
- Migratie On Premise --> Cloud

### PaaS (Platform as a Service)
- **Geen systeembeheerder** nodig
- Ontwikkelaar maakt applicatie en "plaatst" deze op Cloud platform
- Platform beheert servers, hosting, back-ups, scaling
- Zeer veel **flexibiliteit**

*ASP.NET Core, nodejs, python, Java, php*
*AWS, Microsoft Azure, IBM Bluemix, Heroku, Google Cloud*

### SaaS (Software as a Service)
- Software draait meestal niet lokaal
- Betalen per maand/per gebruiker
- Flexibele abonnementen, snel op te zetten
- Geen rekening houden met back-ups en uptime

*Office365, OneDrive, Dropbox, Adobe CC, Google Drive, Gmail, iCloud*

### 3 Vendors
![AWS, Azure, Google Cloud](https://i.imgur.com/k0A4FL9.png)

**Amazon AWS**
*coursera, Atlassian, IMDb, Lamborghini, FCBarcelona, Netflix, Spotify, Airbnb, Autodesk…*

**Azure Cases**
*hp, BMW, Adobe Creative Cloud, Sodexo, G&J Pepsi, M&M’s*

**Google Cloud**
*Coolblue, Philips, Ferrero, Red Bull, Airbus*

**Overige**
Tencent Cloud, IBM, Oracle, Alibaba Cloud

## Microsoft Azure
**Waarom?**
- Zowel .NET als Open Source (PHP, Java, Node, Python, Flask, Docker...)
- Meeste opties en mogelijkheden
- Zeer lage instapdrempel voor studenten

**Waarvoor AWS gebruiken?**
Cloud Services (Smart Tech & Infrastructure)

**Waarvoor Google Cloud Platform gebruiken?**
Kan in projectweken, vooral AI projecten

### Azure Portal
Portal gebruikt voor het beheren van Cloud services en applicaties.

### Azure Subscription
**Abonnement** 
Zal bepalen hoe ze factureren

  - Credits op voorhand
  - Pay by use

In de praktijk: Subscription per klant

## Resource Group
**Logische container**
![Account, Subscription, Resource groups](https://i.imgur.com/C4WiSOx.png)
- Per project
- Per soort service (Storage; Webservers; Fileservers; SQL, Blob...)
- *Kies je zelf*

+ Container met inhoud in één keer verwijderen
+ Toegangsrechten per container

## Azure Virtual Machines
- Eigen server op Azure omgeving
- Meestal migratie On-premise

+ Heel wat mogelijkheden 
*(file servers, database servers, webservers, application servers...)*
+ Toegang tot resources op server die niet mogelijk zijn via web applicatie 
*(Communicatie met oude softwarepakketten; Genereren van Word/Excel documenten)*

- Wanneer je **volledige controle** wenst
- **Volledige controle = volledige verantwoordelijkheid**

### Planned maintenance
- Updates van het Azure platform
  - Stabiliteit
  - Security
  - Performantie
- Soms herstarten

### Unplanned maintenance
- Storing in onderliggende architectuur
  - Netwerk problemen
  - Disk problemen
  - Rack problemen
- Automatische verplaatsing naar werkende infrastructuur

### Availibility Set
- VM "up and running" houden.
  - Garantie vna 99,95% uptime
  - Minstens 2 VM's nodig
  - Duurder

## Azure Web App
- Azure Platform Service
- Web apps online plaatsen
- ~~Eigen server~~
- ~~Webserver configuratie~~

+ Ondersteuning voor
  + ASP.NET (Core)
  + PHP
  + Python Flask
  + Java
  + NodeJS
  + ...

- Easy deployment
- Eenvoudig te koppelen aan Github Repo
- Autoscale (not Free)
- Monitoring
- Staging mode

| FREE | SHARED | BASIC, PREMIUM | ... |
| -- | -- | -- | -- |
| Gedeelde server | Gedeelde server | App Service Plan: eigen server | |
| 1GB Storage | 1GB Storage | SSL | |
| Beperkte trafiek (165MB/dag) | Mogelijkheid tot DNS: custom domains | Mogelijkheid tot DNS: custom domains | |
| | | CPU keuze, Memory keuze | |
| | | Scaling tot 3 toestellen | |

### Scaling
| Scale Up | Scale Out |
| -- | -- |
|Vertical Scaling | Horizontal Scaling |
| = Servers krachtiger maken, meer memory en CPU | = Meerdere machines, maar minder krachtig |
| + Minder energie dan SO | + Goedkoper |
| + Eenvoudiger te implementeren | + Betere bescherming (hardware failure) |


<!--stackedit_data:
eyJoaXN0b3J5IjpbNzk0Mzk1MjA1LDE5MTM1MTQwMF19
-->