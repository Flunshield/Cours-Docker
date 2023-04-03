Mise en contexte :
	- Quelqu'un dev sur son poste
	- Quelquy'un d'autre teste la solution
	- On envoie chez le client 
	- On recommence

Rendre la solution indépendante
	Démarrer rapidemebt la solution
		Transferer facilement la solution
		Rendre la prod et l'environnement du dev casiment identique

Docker isole jusqu'a la couche réseau.

# Docker containers
Un container contient une application avec toutes les dépendances avec toutes les dépendances et els configurations nécéssaires pour qu'elle fonctionne.
	Un container est portable, facilement, copiable ou déplacable vers une autre machine.
L'objectif est de rendre le développement ainsi que le déploiement plus efficace.

Les containers se trouvent dans :
- Les repositorys
- Repository privé
- Repository public => Docker hub [Lien des containers officiel](https://hub.docker.com/)

Une commande pour els démarrer.

ssh -p 9091 ubuntu@isitech.tancou.fr
isipassword
ssh -L 8080:127.0.0.0:8080 -p 9091 ubuntu@isitech.tancou.fr

Installer une image : 
```docker
//Installer une image
docker pull [nom de l'image]

//Lancer une image si pas d'container en local, ira récupéré depuis docker hub par défaud
docker run [nom de l'image]

// Connaitre la liste des container en cours d'éxécution 
docker ps

//arrété un docker 
exit

//afficher la liste des container stocké en local :
docker ps -a

//supprimer un container
docker rm [id ou nom du container (pas obligé de tout taper)]

//afficher els images 
docker images

//Afficher toutes les images 
docker image ls

//mode interractif
docker run -it [nom de l'image] bash

//Exécuter une commande dans un conteneur en cours d'exécution
docker exec

Pour spécifier une vers, rajouter ":xx.xx" a la suite du nom de l'image.

La commande "docker run --rm -it" est utilisée pour lancer un conteneur Docker en mode interactif avec le terminal TTY. Voici ce que signifient les options de la commande :

docker run --rm -it ubuntu bash

```

Un container meurt à l'arret du logiciel. Il a besoin d'un processus pour vivre.

Un container créer une instance de l'image.

-   `docker run` : commande pour lancer un conteneur Docker
-   `--rm` : option pour supprimer automatiquement le conteneur lorsqu'il est arrêté (utile pour éviter l'accumulation de conteneurs inutiles)
-   `-it` : options pour lancer le conteneur en mode interactif avec le terminal TTY (permet d'interagir avec le conteneur via le terminal de la machine hôte)

Pour créer un volume :

```docker
docker run -it -v ubuntu bash
```

ngnix concurrent de appache

# Ngnix
appache = usa
ngnix = russe

[ngnix](https://www.nginx.com/)

Port 80 : Port par défaud web.

```bash
docker run --rm -d -p 8080:80 nginx

--rm : supprime le contnaire a la fin
-d : mode détaché
-p : configuration du port
8080 : port du contnaire
80: port de nginx 
```


Commande utilisé lors d'un tp :

```bash
docker run --rm -d -p 8080:80 -v "C:\Users\jbert\Documents\ISITECH\Cours-Docker\app:/usr/share/nginx/html" nginx
```

==> Créer un index.html dans app
==> /usr/share/nginx/html = fournit dans la doc

Lancer dans un navigateur http://localhost:8080/

# Docker compose

```bash
version: "3"
services:
  web:
    image: nginx
    ports:
      - 8080:80
    volumes:
      - ./app:/usr/share/nginx/html
```

La commande `docker compose up` permet de lancer le fichier docker-compose.yaml et qui exécute tout les dockers renseigné dans celui-ci.

La commande `restart: always` permet de relancer le container avec la même commande.

**Le fichier .yaml décrit les commande docker**

[example de variable d'environnement](https://github.com/docker/awesome-compose)

# Docker file (construction d'image)

Le docker file commence par un D en MAJUSCULE !

Le DockerFile doit partir forcément d'une couche, en général, elle part de la couche primaire (la plus basse est scratch)

FROM : Cette commande spécifie l'image de base à partir de laquelle vous construisez votre image Docker
WORKDIR : Cette commande définit le répertoire de travail dans lequel les commandes suivantes seront exécutées.
RUN : Cette commande exécute des commandes dans l'image Docker pendant le processus de construction.
BUILD : La commande `docker build` permet de construire une image Docker à partir d'un fichier Dockerfile.
```docker
docker build -t TP_DOCKER_FILE:1.0.0 .
```

Le "." fais référence dans le dossier où nous sommes présent.

COPY . . = La commande `COPY . .` est une instruction du Dockerfile qui permet de copier tous les fichiers et dossiers du répertoire de construction local (ou "contexte" Docker) vers le répertoire de destination dans l'image Docker en cours de construction.

```bash
COPY ./app /app = COPY ./app .
```

Pour spécifier la dernière version :
```
docker tag SOURCE:tag (test:2.0.0) DESTINATION:tag (test:latest)
```

En faisant cela, lorsque nous exécuterons al commande docker run, nous pourrons tout simplement indiqué "latest" sur le numéro de version.

la commande ``pwd`` permet de connaitre le chemin.

en python il faut le requirements.txt

Les commandes s'éxécute dans un array de paramètre. 
```
["python3", "app.py"]
```

Si build 2x d'affiler, la deuxième fois, ca build instantanément.

Il faut ordonner ses sources afin d'optimiser les builds. (Gros gain de temps en prod)
==> LEs dépendances en 1er

```bash

```