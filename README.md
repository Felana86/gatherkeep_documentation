# gatherkeep_documentation

Gatherkeep est une application web full-stack, qui me sert de bac à sable pour explorer et évoluer tout au long de mon apprentissage.
Il s'adresse auxhabitants et associations d'une ville, d'une commune ou d'un village. 
C'est une plateforme collaborative pour redonner du sens à l'engagement de proximité.

# Architecture

Ce projet utilise une architecture distribuée avec :

* __Backend__ : API REST avec authentification JWT
* __Frontend__ : Interface utilisateur moderne
* __Base de données__ : MySQL 8.0
* __Proxy__ : Nginx avec SSL automatique
* __Déploiement__ : Docker & Docker Compose

## Structure des dépôts

Projet GatherKeep (3 dépôts séparés)

├── gatherkeep-backend/     # API + logique métier

├── gatherkeep-frontend/    # Interface utilisateur

└── gatherkeep-docs/        # Documentation centralisée (ce dépôt)

# Démarrage rapide

## Développement local

1. Cloner les dépôts backend et frontend
2. Suivre les instructions dans [local-development.md](./local-development.md)

## Production

1. Configuration serveur détaillée dans [production-deployment.md](./production-deployment.md)
2. Docker Compose de production dans [docker-compose-production.md](../deployment/docker-compose-production.md)

# Documentation

## Architecture

* __[Vue d ensemble](#Structure des dépôts)__ - Architecture générale et choix techniques
* __[Développement local](./local-development.md)__ - Setup en local
* __[Déploiement production](./production-deployment.md)__ - Configuration serveur

## Services

* __[Backend](../services/backend.md)__ - API, authentification, base de données
* __[Frontend](../services/frontend.md)__ - Interface utilisateur
* __[Base de données](../services/database.md)__ - MySQL, structure, migrations
* __[Nginx](../services/nginx.md)__ Reverse proxy, SSL, configuration
* __[Certbot](../services/certbot.md)__ - Gestion automatique des certificats SSL

## Déploiement

* __[Docker Compose Production](../deployment/docker-compose-production.md)__ - Configuration complète

# Technologies utilisées

## Backend :

* __TypeScript - NestJS - Prisma__
* __MySQL 8.0__
* __JWT pour l'authentification__

## Frontend :

* __React - TypeScript - ViteJS__
* __Cypress__
* __Zustand__

## Infrastructure :

* __Docker & Docker Compose__
* __Nginx__
* __Let's Encrypt (Certbot)__
* __Serveur OVH__

# Développement

## Prérequis

* __Docker & Docker Compose__
* __Autre__

## Installation

Voir [Développement local](./local-development.md) pour les intructions détaillées.

## Statut du projet

* __Backend API fonctionnel__
* __Frontend opérationnel__
* __Base de données configurée__
* __Déploiement production__
* __Documentation en cours__
* __Autres fonctionnalités en cours__

## Contact

email: felana_letrange@fastmail.com

----------------------------------------------------------------------------------------------------------------------

Cette documentation est maintenue à jour avec l'évolution du projet.