# 1 - Intro Azure Cloud
## Wat is Cloud Computing

![Van On premise tot SaaS](https://i.imgur.com/Ne9mMxp.png)

### On Premise (eigen servers)
- IT afdeling **verantwoordelijk voor ALLES**
  - *Back-up + recovery, aankoop hardware, scaling*
- **Investeren in hardware** die je beperkt nodig hebt (*bv. kerst*)
- **Vrijheid**
- Soms **verplicht door wetgeving**
  - *Medische / financiële data*
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
: Zal bepalen hoe ze factureren

- Credits op voorhand
- Pay by use

+ *In de praktijk: Subscription per klant*


## Resource Group
![Account, Subscription, Resource groups](https://i.imgur.com/C4WiSOx.png)

Logische container
: Per project
: Per soort service *(Storage; Webservers; Fileservers; SQL, Blob...)*
: ...

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

## Scaling
Scale Up 
: Vertical Scaling
: Server krachtiger maken, meer memory en CPU

+ ✅ Minder energie dan Scale Out
+ ✅ Eenvoudiger de implementeren
+ ✅ Minder licenties (n.v.t. voor Azure Web App)
- ❌ Duurder
- ❌ Hardware failure => Toepassing down

Scale Out
: Horizontal Scaling
: Meerdere machines, maar minder krachtig

+ ✅ Goedkoper
+ ✅ Betere bescherming (hardware failure)
- ❌ Meer licenties (n.v.t. voor Azure Web App)
- ❌ Meer plaats in datacenter
- ❌ Meer energy
- ❌ Complexer netwerk
- ❌ Soms toepassingen aanpassen

## Azure SQL
- SQL Server Database op Cloud platform
- Zelf geen hardware/software aankopen
- Niet verantwoordelijk voor backups
- Eenvoudig schalen bij zware loads

| Serverless Managed Database | SQL Managed Instance | SQL Virtual Machine |
| -- | -- | -- |

- SQL Server Cloud Based
  - Compatible met SQL Server 2012
  - Te beheren via Enterprise Manager
  - Werkt zoals een gewone SQL Server
  - Connecteren mogelijk via *.NET, Python, PHP, Node…*
  - High Availability
    - Replicatie over drie servers (default)
    - Automatic Back-ups
---
 - Database draait op een server
- Verschillende pricing mogelijkheden
---
 - Security: IP Adres instellen in Firewall
---
### Azure DTU
Database Transaction Units
: CPU
: Memory
: I/O

Hoe meer DTU, hoe meer power, hoe duurder

### Throttling
Het onderbreken van database communicatie omdat je teveel resources gebruikt.
*Zelf voor retry zorgen.*

![Throttling types](https://i.imgur.com/1R4Y5Zw.png)

![Throttling modes](https://i.imgur.com/t4mYuN2.png)
Niet vanbuiten kennen.

### Azure Database for MySQL
- Toegang via MySQL Workbench
- Werkt zoals een gewone MySQL
- Geen eigen servers
- Automatische back-up

## Azure & Internet of Things
**Waarom is Azure zo belangrijk voor IoT?**
|||
|--|--|
| Azure Event Hubs | Ontvangen van berichten afkomstig van toestellen |
|Azure IoT Hub | Ontvangen van berichten |
|| Sturen van berichten naar toestellen |
|Azure Streaming Analytics | Verwerken van events afkomstig van Event Hubs en IoT hub |
*Event Hubs en IoT hub kunnen miljoenen berichten per seconden aan.*

![Microsoft Services](https://i.imgur.com/UwgLGFE.png)

## Azure CLI
Azure Portal
: Dagelijks gebruik
: Niet makkelijk te automatiseren
: Wat bij 100 sites?
: Wat bij 50 servers?

Oplossing: Azure CLI 2.0
: Commandline > Resources aanmaken
: Makkelijk via scripts
: Ideaal voor DevOps

## Bash / Powershell
Bash commandline in portal
Alles wat je via UI kan, kan via commandline in portal

## Belangrijk

 - Weten wat Cloud computing is?
 - Wie zijn de grote spelers?
 - Welke soorten zijn er en wat zijn hun eigenschappen? + voorbeeld
 - Wat is een Azure subscription?
 - Wat zijn resource groups?
 - Hoe kan je scalen?
 - Voor- en nadelen van Azure VM’s?
 - Wanneer Azure VM gebruiken?
 - Wat is SQL Azure en wat zijn DTU’s?
 - Wat is throttling?
 - Wat is een Azure Web App?
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAxNDM4MTAwNiwtNzMxNDIyNzEwLDEzMT
YzNTU4NjEsMTI4NDU5NjU0NSwyMDgxNTAxMzA4LC0xMTg0NzM4
MDY0LC0xODU1NjY5MzYxLC04NTk5MTYyOTIsLTE0MTg5Mzk0OD
QsLTI0MDA4ODk4MywtNjA5ODQyNTI4LDMxNzYxNjY2MCwtMTc5
MTU5OTc1OCwxOTEzNTE0MDBdfQ==
-->