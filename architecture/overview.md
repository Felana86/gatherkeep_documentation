# Archtiecture Overview Gatherkeep

## Vue d'ensemble

Gatherkeep utilise une architecture distribuée moderne qui sépare clairement les responsabilités entre le frontend, l e backend, et l'infrastructure.
Cette approche offre une meilleure maintenabilité, une scalabilité accrue, et permet un développement en équipe plus efficace.

## Architecture générale 

### PRODUCTION (OVH)

#### Nginx (port 80/443)

* __SSL Termination (Let's Encrypt)__
* __Static Files (Frontend)__
* __Reverse Proxy --> Backend API__

#### Frontend Container 

* __Interface utilisateur__

#### Backend Container (Port 3000)

* __API REST__
* __Authentification JWT__
* __Logique métier


#### MySQL Container (Port 3306)

* __Base de données principale__


#### PhpMyAdmin (Port 8090)

* __Interface d'administration DB__


## Structure des dépôts

### Pourquoi 3 dépôts séparés ?

#### 1. Séparation des préoccupations :

* __Backend :__ Logique métier, API, sécurité
* __Frontend :__ Interface utilisateur, expérience utilisateur
* __Documentation :__ Architecture, déploiement, maintenance

#### 2. Déploiement indépendant :

* __Equipes peuvent travailler en parallèle__
* __Cycles de déploiement indépendants__
* __Gestion des versions séparées__

#### 3. Réutilisabilité :

* __Backend peut servir plusieurs frontends (web, mobile, etc.)__
* __Frontend peut être déployé sur différents environnements__
* __Documentation centralisée pour tous les environnements__


## Flux de développement 

### Environnement local 

    Développeur
    ├gatherkeep-backend/ (Port 3000)
    |   ├docker-compose.yml # MySQL + Backend
    |   └Dockerfile
    ├gatherkeep-frontend/ (Port 5173/3001)
    |   ├docker-compose.yml # Frontend seul
    |   └Dockerfile.dev
    └Communication directe Frontend -> Backend

### Environnement de production 

    Serveur OVH
    ├docker-compose.yml # Orchestration complète
    ├Images built depuis les dépôts
    └Nginx comme point d'netrée unique

## Communication entre services

### En développement local

* __Frontend communique directement avec backend via__  http://localhost:3000
* __Base de données accessibles via__ http://localhost:3306
* __PhpMyAdmin accessible via__ http://localhost:8090

### En prodcution 

* __Nginx reçoit toutes les requêtes (ports 80/443)__
* __Requ^tes API proxifiées vers le backend__
* __Fichiers statiques servis directement par Nginx__
* __Communication interne via le réseau docker__


## Technologies et choix techniques

### Base de données : MySQL 8.0

#### Pourquoi MySQL ?

* __Performance éprouvée pour les applications web__
* __Ecosystème mature (PhpMyAdmin, outils de monitoring)__
* __Compatibilité avec la stack backend__
* __Support natif des transactions ACID__

### Reverse Proxy : Nginx

#### Pourquoi Nginx ?

* __Performance exceptionnelle pour servir les fichiers statiques__
* __Proxy inverse efficace__
* __Configuration SSL simplifiée__
* __Gestion du cache intégrée__
* __Equilibrage de charges si nécessaire plus tard__

### Conteneurisation : Docker

#### Avantages :

* __Environnements reproductibles__
* __Isolation des services__
* __Déploiement simplifié__
* __Scalabilité horizontale future__

### SSL : Let's Encrypt + Certbot

#### Pourquoi cette solution ?

* __Certificats gratuits et automatiques__
* Renouvellement automatique__
* __Standard de l'industrie__
* __Configuration zero-downtime__

### Sécurité 

#### Authentification 

* __JWT avec tokens d'accès (15 min) et de refresh (7 jours)__
* __Secrets stockés dans des variables d'environnement__
* __Hash des mots de passe côté backend__

#### Réseaux 

* __Services isolés dans des réseaux Docker dédiés__
* __Exposition minimale desports__
* __SSL/TLS obligatoires en production__

#### Base de données 

* __Accès restreint au réseau Docker interne__
* __Mots de passe forts stockés en variables d'environnement__
* __PhpMyAdmin accessible uniquement en interne__

### Evolutivité

Cette architecture permet facilement :

* __Scaling horizontale :__ Ajout de containers backend/frontend
* __Microservices :__ Séparation future en services métier
* __CDN :__ Ajout d'un CDN devant Nginx
* __Cache :__ Intégration d'outils comme Prometheux/Grafana

#### Avantages de cette architecture

1. __Maintenabilité :__ Code organisé, responsabilités claires
2. __Fléxibilité :__ Déploiement et développement indépendants
3. __Performance :__ Nginx optimisé, conteneurs légers
4. __Sécurité :__ Isolation, SSL, authentification robuste
5. __Développement :__ Setup local simple, documentation centralisée

#### Prochaines évolutions possibles

* Migration vers des microservices spécialsés
* Ajout d'un cache Redis
* Intégration CI/CD automatisée
* Monitoring et alerting
* Tests automatisés end-to-end
