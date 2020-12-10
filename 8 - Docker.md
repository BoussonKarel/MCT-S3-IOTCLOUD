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
- PC/Mac/Linux omgevingen in één team
- Deployment op RPi
- ... zolang er maar een Docker Engine aanwezig is

## Hoe werkt Docker?
| Docker Image | Docker Container |
|--|--|
| Snapshot van files in een Linux file system | Runtime instantie van een container (container image) |
| Basis van Image is een Linux OS (Windows kan maar zien we niet) | Containers geïsoleerd van elkaar, maar kunnen communiceren naar buiten toe |
| Via een Dockerfile kunnen we een Docker image aanmaken | Volledige toegang tot CPU en memory |
| Bevat de ontwikkelde applicaties en de libraries die er nodig zijn | |

Docker Hub
: Public repo met images

Docker Client
: Programma op PC developper voor aanmaken Docker Images
: Volledig command line

- Wanneer een Docker Image klaar is:
  - Push naar docker registry
    - Docker Hub
    - Azure Container Registry
  - Container opzetten in Cloud omgeving op basis van Image uit de Registry

![](https://i.imgur.com/HE9awAO.png)

## Basiscommando's
| Docker commando | |
|--|--|
| docker pull nginx | Download image "nginx" van Docker Hub |
| docker images | Overzicht images op het systeem |
| docker run -p 80:80 nginx | Opstarten van container op basis van image nginx en poort 80 [container] mappen naar poort 80 [host] |
| docker ps | Overzicht containers die actief zijn |
| docker ps -all | Overzicht van alle containers |
| docker exec -it 6becfdf32737 bash | Inloggen in container met bash shell |
| docker stop | Stoppen van container |
| docker rm | Verwijderen van container |
| docker rmi | Verwijderen image |

## Dockerfile
File zonder extensie met als naam "Dockerfile"

**Beschrijft build proces image**
```docker
FROM tiangolo/uwsgi-nginx-flask:python3.6
```

Via RUN commando kunnen we extra bibliotheken installeren die de applicatie nodig heeft om te werken
```docker
RUN apt-get update
RUN pip install --upgrade pip
RUN pip install pandas
RUN pip install matplotlib
RUN pip install numpy
```

We moeten ook de applicatie naar de image kopiëren
```docker
COPY ./app /app
# (bron op pc) (doel in container)
```

## Build Image
```
docker build -t demonmct:first
# -t = tag toevoegen na de : (bv. first)
```

## Run container
Opvragen van de images met ```docker images```

Starten van een image ```docker run -p 80:80 -t demonmct:first```

Stoppen van een image ```docker stop <container-id>```

## Push naar Azure Container Registry
Azure Container Registry
: Private repository voor Images
: Image uploaden voor we deze online kunnen zetten

Eerst inloggen in de private registry
```az acr login -name iotcloudles```

Voor we kunnen pushen moeten we de image taggen
```
docker tag demonmct:first iotcloudles.azurecr.io/demonmct
# naam image lokaal (demonmct) + tag voor private repo (moet URL repo bevatten)
```

```
docker push <url>/<naam image>
```

## Deploy Container Azure
Azure Web App for Containers

## Docker Compose
- Wat als we meerdere docker containers nodig hebben voor onze applicatie?
- Cache Server
- Data

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
eyJoaXN0b3J5IjpbMTg4MTE3NjY3OSwtMTEzMzgyMDc0OCwxMz
cyMDMzMTc4LC0xMDMxNDcyNjk2LDE3Mzg4MDcwNjksODI1MzIy
ODY4LDE3MTkzMDc3MTAsNjYyNTA3NjYsLTE1NjE0NjM1NjEsOD
QzNTIxMTksMTQzMjYzNDYxMl19
-->