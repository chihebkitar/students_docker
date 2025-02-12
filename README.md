# Student List App (Python Flask + PHP)

## Description

Cette application est composée de deux modules :

- **API Python/Flask** : Fournit une liste d'étudiants et leurs âges à partir d'un fichier JSON.
- **Site web PHP** : Permet d'afficher la liste des étudiants en consommant l'API.

L'objectif est de déployer chaque module dans des conteneurs Docker distincts et de les orchestrer avec Docker Compose.

## Prérequis

- [Docker](https://docs.docker.com/get-docker/) et [Docker Compose](https://docs.docker.com/compose/install/) installés
- (Optionnel) [Vagrant](https://www.vagrantup.com/docs/installation) pour exécuter l'environnement dans une machine virtuelle

## Arborescence du projet

```
student_list/
  ├── simple_api/
  │   ├── Dockerfile
  │   ├── student_age.py
  │   └── student_age.json
  ├── website/
  │   └── index.php
  └── docker-compose.yml
```

## Installation et exécution

### 1. Démarrer la VM Vagrant

Si vous souhaitez exécuter le projet dans une VM Vagrant :

```bash
vagrant up --provision
vagrant ssh
```

### 2. Construire l'image de l'API

Accédez au dossier `simple_api` et construisez l'image Docker :

```bash
cd simple_api
docker build -t api:v1.0 .
```

### 3. Lancer l'application avec Docker Compose

Revenez à la racine du projet et lancez les conteneurs :

```bash
cd ..
docker compose up -d
```

Cela crée deux services :

- **api** : le serveur Flask qui expose l'API sur le port 5000
- **webpage** : le site PHP accessible sur le port 80

## Utilisation

1. Ouvrez votre navigateur et accédez à :
   ```
   http://localhost/
   ```
   ou, si vous utilisez Vagrant :
   ```
   http://192.168.56.5/
   ```
2. Cliquez sur le bouton **List Student** pour voir la liste des étudiants.

## Configuration

- L'authentification de l'API est gérée par **HTTP Basic Auth**. Les identifiants par défaut sont :
  - **Username** : `toto`
  - **Password** : `python`
- Dans `website/index.php`, l'URL de l'API est configurée comme suit :
  ```php
  $url = 'http://api:5000/pozos/api/v1.0/get_student_ages';
  ```

## Bonnes pratiques et améliorations

- **Fichier requirements.txt** : Externalisez les dépendances Python dans un fichier `requirements.txt`.
- **Sécurisation** : Utilisez un proxy inverse (comme Nginx) pour ajouter du HTTPS.
- **Optimisation Docker** : Nettoyez les caches d'installation pour réduire la taille des images.

## Licence

Ce projet est sous licence MIT.


