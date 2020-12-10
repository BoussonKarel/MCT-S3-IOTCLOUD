# 8 - Docker
- Wat is Docker?
- Waarom Docker?
- Basiswerking
- Wat is de DockerFile
- Docker Registry
- Basiscommando's
## Wat is Docker?
### Deployment van applicaties
**Oude manier** van deployment (installatie van de applicatie)
- Verschillende applicaties op één server.
- Server bevat alle nodige libraries die alle applicaties nodig hebben
- Zeer lastig om te beheren (nieuwe versies, maar niet alles updaten)
- Applicaties NIET gescheiden van elkaar
- Veel werk bij update uitrollen
- Altijd systeembeheerder nodig om updates uit te rollen

![](https://i.imgur.com/a8A94Ez.png)

**Nieuwe manier** van deployment (installatie van de applicatie)
- Applicatie met nodige libraries in een image, die we kunnen opstarten als container
- Alle applicaties gescheiden van elkaar, delen enkel kernel van OS
- Geen versie conflicten tussen libraries
- Makkelijker updates, gewoon update van de image en container heropstarten
- Geen systeembeheerder nodig

![](https://i.imgur.com/4tGUd33.png)

![](https://i.imgur.com/cfKFyZ9.png)

## Waarom Docker?
Eenvoudiger software distribueren
- Verplaatsen workload naar Cloud
- Meer en meer gebruik van verschillende platformen binnen 1 applicatie
- Willen ons niet koppelen aan 1 Cloud > Vendor locking vermijden
- Azure, Amazon, Google... allemaal ondersteuning voor Docker
- We moeten onze code NIET aanpassen, gewoon container aanpassen

**Docker scenario's**
- Custom ML / Deep Learning model draaien in cloud omgeving
  - Toegang tot GPU vanuit Docker enkel op Linux
- Als je Cloud vendor neutraal wil zijn
- Dev Ops deployments
- Nieuwe technologie verkennen zonder uw machine te vervuilen
- PC

## Hoe werkt Docker?

## Basiscommando's

## Dockerfile

## Build Image

## Run container

## Push naar Azure Container Registry

## Deploy Container Azure

## Docker Compose

## Docker Volumes

## Belangrijk
- Wat is docker?
- Waarom dockergebruiken ?
- Wat is een DockerFile?
- Wat is docker-compose?
- Wat is DockerHub?
- De basiscommando’s weten wat ze doen, maar niet alle parameters
- Wat zijn de manieren om bij docker applicaties correcte de data te kunnen wegschrijven?
-   Wat zijn volumes?
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzM2Mjk0NDI4LDE3MTkzMDc3MTAsNjYyNT
A3NjYsLTE1NjE0NjM1NjEsODQzNTIxMTksMTQzMjYzNDYxMl19

-->