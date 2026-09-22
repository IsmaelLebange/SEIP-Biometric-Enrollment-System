# SEIP — Système d'Enrôlement des Identités des Personnes

## Présentation

SEIP est un système d'enrôlement biométrique permettant d'enregistrer les informations civiles des citoyens et de réaliser une vérification biométrique à l'aide de la reconnaissance faciale et des empreintes digitales.

Le projet a été développé dans un contexte académique avec une architecture orientée vers la séparation des responsabilités, la maintenabilité et l'évolution du système.

L'application repose sur :

* un backend REST développé avec Django et Django REST Framework ;
* une application mobile développée avec React Native et Expo ;
* un système de gestion des données civiles et biométriques ;
* des mécanismes d'authentification, de validation et d'audit ;
* une architecture inspirée de Clean Architecture et du Domain-Driven Design.

## Fonctionnalités

### Enrôlement

* Création du profil d'un citoyen
* Enregistrement des informations personnelles
* Gestion des adresses et divisions administratives
* Validation des données d'enrôlement

### Biométrie

* Capture d'image depuis l'application mobile
* Traitement d'image avec OpenCV
* Reconnaissance faciale
* Gestion des données biométriques
* Vérification de l'état de complétion de l'enrôlement biométrique

### Gestion des citoyens

* Consultation du profil
* Gestion des documents
* Validation administrative
* Génération de QR codes

### Sécurité et traçabilité

* Authentification JWT
* Gestion sécurisée des mots de passe
* Validation des données côté API
* Journalisation des actions
* Transactions atomiques pour garantir la cohérence des opérations

## Architecture

Le backend suit une organisation inspirée de Clean Architecture et du Domain-Driven Design.

```text
                 Mobile Application
                  React Native / Expo
                         |
                         | REST API
                         v
              +-----------------------+
              |   Presentation / API  |
              +-----------------------+
                         |
                         v
              +-----------------------+
              |   Application Layer  |
              | Services / Providers  |
              +-----------------------+
                         |
                         v
              +-----------------------+
              |      Domain Layer     |
              | Entities / Value      |
              | Objects / Services     |
              +-----------------------+
                         |
                         v
              +-----------------------+
              | Infrastructure Layer  |
              | Repositories /        |
              | External Services     |
              +-----------------------+
                         |
                         v
                    Database
```

## Backend

Le backend est développé avec Python, Django et Django REST Framework.

Il est organisé autour de plusieurs responsabilités :

```text
backend/
├── config/
│   ├── settings.py
│   └── urls.py
├── src/
│   ├── apps/
│   │   ├── api/
│   │   │   ├── controllers/
│   │   │   ├── providers/
│   │   │   └── serializers/
│   │   ├── services/
│   │   ├── repositories/
│   │   └── interfaces/
│   ├── domain/
│   │   ├── entities/
│   │   ├── value_objects/
│   │   └── exceptions/
│   ├── shared/
│   │   ├── config/
│   │   ├── external_services/
│   │   ├── logging/
│   │   ├── security/
│   │   └── utils/
│   ├── migrations/
│   └── requirements/
├── tests/
└── manage.py
```

### Principales entités

Le domaine métier comprend notamment :

* Citoyen / User
* Adresse
* Données biométriques
* Document
* Province
* Territoire
* Secteur / Chefferie
* Partenaire
* AuditLog
* OTP

## Frontend mobile

L'application mobile est développée avec React Native et Expo.

```text
frontend/
├── src/
│   ├── api/
│   ├── components/
│   ├── constants/
│   ├── hooks/
│   ├── navigation/
│   ├── screens/
│   ├── services/
│   └── store/
├── assets/
├── App.js
├── app.json
└── package.json
```

L'application comprend notamment :

* écrans d'authentification ;
* formulaire d'enrôlement ;
* capture d'image ;
* consultation du profil ;
* gestion des documents ;
* validation administrative ;
* consultation des informations d'enrôlement.

## Capture biométrique

La caméra du terminal mobile est utilisée pour capturer les données nécessaires au traitement biométrique.

Le flux général est :

```text
Capture mobile
      |
      v
Image biométrique
      |
      v
API Django REST
      |
      v
Traitement biométrique
      |
      v
Validation / stockage
```

OpenCV est utilisé côté backend pour les traitements liés à la reconnaissance faciale.

## API

Quelques endpoints principaux :

```text
POST /api/auth/login/
POST /api/auth/register/
POST /api/auth/otp/
POST /api/auth/logout/

POST /api/enrollment/
POST /api/enrollment/complete/

POST /api/biometric/enroll/

GET  /api/profile/
GET  /api/qr/

GET  /api/admin/citizens/
```

## Technologies

### Backend

* Python
* Django
* Django REST Framework
* OpenCV
* JWT
* SQLite pour le développement
* PostgreSQL prévu pour la production

### Frontend

* React Native
* Expo
* JavaScript
* Axios
* React Navigation
* Context API

### Architecture et conception

* Clean Architecture
* Domain-Driven Design
* SOLID
* Repository Pattern
* Service Layer
* Factory Pattern
* Strategy Pattern

## Tests

Le projet comprend plusieurs niveaux de tests :

* tests unitaires des entités et services métier ;
* tests d'intégration des API ;
* tests fonctionnels du parcours d'enrôlement.

L'objectif est de vérifier à la fois la logique métier et l'intégration entre les différentes couches du système.

## Sécurité

Le projet traite des données personnelles et biométriques. Les mécanismes étudiés comprennent notamment :

* authentification JWT ;
* hachage des mots de passe ;
* validation des données ;
* contrôle des accès ;
* audit logging ;
* transactions atomiques ;
* gestion des variables sensibles par variables d'environnement.

Ce projet est académique et ne doit pas être utilisé pour traiter de véritables données biométriques sans une analyse de sécurité, de conformité et de protection des données adaptée à un environnement de production.

## Installation

### Backend

```bash
cd backend

pip install -r requirements/development.txt

python manage.py migrate
python manage.py runserver
```

### Frontend

```bash
cd frontend

npm install
npx expo start
```

L'application peut ensuite être exécutée avec Expo sur un appareil mobile compatible.

## Objectifs techniques

Ce projet a principalement permis de travailler sur :

* conception d'API REST ;
* architecture logicielle ;
* Clean Architecture ;
* Domain-Driven Design ;
* développement backend avec Django ;
* développement mobile avec React Native ;
* traitement d'images avec OpenCV ;
* authentification et sécurité des API ;
* gestion de données sensibles ;
* tests logiciels ;
* séparation des responsabilités et maintenabilité du code.

## Contexte académique

Projet réalisé dans le cadre du cursus de Master en Intelligence Artificielle.

Le projet met l'accent sur l'intersection entre intelligence artificielle, développement logiciel et conception d'applications distribuées.

## Auteur

**Ismaël Lebange**

Master en Intelligence Artificielle
