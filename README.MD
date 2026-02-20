<div align="center">

# 🛒 ACME — Plateforme E-commerce

**Une application web e-commerce moderne, full-stack, propulsée par Symfony & React.**

[![PHP](https://img.shields.io/badge/PHP-8.1+-777BB4?style=for-the-badge&logo=php&logoColor=white)](https://php.net)
[![Symfony](https://img.shields.io/badge/Symfony-6.2-000000?style=for-the-badge&logo=symfony&logoColor=white)](https://symfony.com)
[![React](https://img.shields.io/badge/React-16.8-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://reactjs.org)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-336791?style=for-the-badge&logo=postgresql&logoColor=white)](https://postgresql.org)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)
[![API Platform](https://img.shields.io/badge/API_Platform-3.1-E2336B?style=for-the-badge&logo=api-platform&logoColor=white)](https://api-platform.com)

</div>

---

## 📋 Sommaire

- [À propos](#-à-propos)
- [Fonctionnalités](#-fonctionnalités)
- [Stack Technique](#-stack-technique)
- [Architecture](#-architecture)
- [Installation](#-installation)
- [Lancement](#-lancement)
- [Tests](#-tests)
- [Structure du projet](#-structure-du-projet)

---

## 🎯 À propos

ACME est une plateforme e-commerce complète permettant aux utilisateurs de naviguer dans un catalogue de produits (chaussures), de les ajouter à un panier, de passer des commandes et de laisser des avis. Le projet repose sur une architecture **découplée** avec un back-end Symfony exposant une API REST/JSON-LD et un front-end React consommant cette API.

---

## ✨ Fonctionnalités

| Fonctionnalité | Description |
|---|---|
| 🔐 **Authentification** | Inscription, connexion et gestion de session via **JWT** |
| 👟 **Catalogue Produits** | Parcourir, filtrer et consulter les fiches produits |
| 🛒 **Panier** | Ajouter, modifier et supprimer des articles du panier |
| 📦 **Commandes** | Passer une commande et suivre son statut de livraison |
| ⭐ **Avis** | Déposer et consulter des avis sur les produits |
| 👤 **Profil** | Gestion du compte utilisateur |
| 📊 **Stock** | Interface de gestion du stock (admin) |

---

## 🛠 Stack Technique

### Backend
- **[Symfony 6.2](https://symfony.com)** — Framework PHP robuste et moderne
- **[API Platform 3.1](https://api-platform.com)** — Génération d'API REST & JSON-LD
- **[Doctrine ORM](https://www.doctrine-project.org)** — Mapping objet-relationnel
- **[Lexik JWT Bundle](https://github.com/lexik/LexikJWTAuthenticationBundle)** — Authentification stateless par token
- **[Nelmio CORS Bundle](https://github.com/nelmio/NelmioCorsBundle)** — Gestion des cross-origin requests

### Frontend
- **[React 16](https://reactjs.org)** — Interface utilisateur composant-based
- **[React Router DOM v5](https://reactrouter.com)** — Navigation côté client (SPA)
- **[Axios](https://axios-http.com)** — Client HTTP pour les appels API
- **[Material UI](https://mui.com)** — Composants UI accessibles et esthétiques
- **[React Bootstrap](https://react-bootstrap.github.io)** — Mise en page responsive
- **[Font Awesome](https://fontawesome.com)** — Icônes SVG
- **[React Toastify](https://fkhadra.github.io/react-toastify)** — Notifications élégantes

### Infrastructure
- **[PostgreSQL 15](https://www.postgresql.org)** — Base de données relationnelle
- **[Docker & Docker Compose](https://docker.com)** — Conteneurisation et orchestration
- **[Webpack Encore](https://symfony.com/doc/current/frontend.html)** — Pipeline d'assets front-end

---

## 🏗 Architecture

```
ACME/
├── acme/                       # Application principale
│   ├── assets/
│   │   └── js/
│   │       ├── components/     # Composants React réutilisables
│   │       ├── contexts/       # React Contexts (Auth, etc.)
│   │       ├── pages/          # Pages de l'application
│   │       └── services/       # Appels API (Axios)
│   ├── config/                 # Configuration Symfony
│   ├── migrations/             # Migrations Doctrine
│   ├── src/
│   │   ├── Controller/         # Contrôleurs Symfony
│   │   └── Entity/             # Entités Doctrine (Produit, Panier, User…)
│   ├── templates/              # Template Twig (SPA shell)
│   └── tests/                  # Tests PHPUnit & Jest
└── docker-compose.yml          # Orchestration des services
```

---

## ⚙️ Installation

### Prérequis

- [Docker Desktop](https://www.docker.com/products/docker-desktop) (v20+)
- [PHP 8.1+](https://www.php.net/downloads) & [Composer](https://getcomposer.org)
- [Node.js 18+](https://nodejs.org) & npm

### 1. Cloner le dépôt

```bash
git clone <url-du-repo>
cd ACME
```

### 2. Démarrer la base de données

```bash
docker-compose up -d
```

### 3. Installer les dépendances PHP

```bash
cd acme
composer install
```

### 4. Configurer l'environnement

```bash
# Copier le fichier d'environnement
cp .env .env.local
```

Ouvrez `.env.local` et vérifiez / renseignez les variables suivantes :

```dotenv
DATABASE_URL="postgresql://app:!ChangeMe!@127.0.0.1:5432/app"
JWT_SECRET_KEY=%kernel.project_dir%/config/jwt/private.pem
JWT_PUBLIC_KEY=%kernel.project_dir%/config/jwt/public.pem
JWT_PASSPHRASE=your_passphrase
```

### 5. Générer les clés JWT

```bash
php bin/console lexik:jwt:generate-keypair
```

### 6. Créer la base de données & exécuter les migrations

```bash
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
```

### 7. (Optionnel) Charger des données de test

```bash
php bin/console doctrine:fixtures:load
```

### 8. Installer les dépendances JavaScript

```bash
npm install
```

---

## 🚀 Lancement

### Mode développement

**Terminal 1 — Serveur Symfony :**
```bash
cd acme
symfony server:start
```

**Terminal 2 — Webpack (watch mode) :**
```bash
cd acme
npm run watch
```

L'application sera disponible sur : **[http://localhost:8000](http://localhost:8000)**

### Build de production

```bash
npm run build
```

---

## 🧪 Tests

### Tests PHP (PHPUnit)

```bash
cd acme
php bin/phpunit
```

### Tests JavaScript (Jest)

```bash
cd acme
npm run test
```

---

## 🔑 Pages disponibles

| Route | Description |
|---|---|
| `/` | Page d'accueil |
| `/login` | Connexion |
| `/register` | Inscription |
| `/chaussures` | Catalogue des chaussures |
| `/produit/:id` | Fiche produit |
| `/panier` | Mon panier |
| `/commande` | Finaliser la commande |
| `/profil` | Mon profil |
| `/avis` | Avis clients |
| `/stock` | Gestion du stock (admin) |

---

## 📄 Licence

Ce projet est sous licence **propriétaire**. Tous droits réservés.

---

<div align="center">

Fait avec ❤️ — Projet **ACME** · Symfony + React

</div>
