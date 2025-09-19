# BobApp - Application de Blagues avec CI/CD

[![CI/CD Pipeline](https://github.com/NairodP/bobapp-ci-cd/actions/workflows/ci.yml/badge.svg)](https://github.com/NairodP/bobapp-ci-cd/actions/workflows/ci.yml)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=NairodP_bobapp-ci-cd&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=NairodP_bobapp-ci-cd)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=NairodP_bobapp-ci-cd&metric=coverage)](https://sonarcloud.io/summary/new_code?id=NairodP_bobapp-ci-cd)

> **Note** : Ce repository est un fork du projet original OpenClassrooms : [Gerez-un-projet-collaboratif-en-int-grant-une-demarche-CI-CD](https://github.com/OpenClassrooms-Student-Center/Gerez-un-projet-collaboratif-en-int-grant-une-demarche-CI-CD)

## Présentation du Projet

BobApp est une application web simple d'affichage de blagues avec un focus sur l'automatisation CI/CD pour simplifier la maintenance. Le projet comprend :

- **Backend** : API Spring Boot (Java 17)
- **Frontend** : Application Angular 14
- **CI/CD** : Pipeline automatisé avec GitHub Actions
- **Qualité** : Analyse continue avec SonarCloud
- **Déploiement** : Conteneurs Docker sur Docker Hub

## Structure du Projet

```
bobapp-ci-cd/
├── back/                           # Backend Spring Boot
│   ├── src/
│   │   ├── main/java/             # Code source Java
│   │   │   └── com/openclassrooms/
│   │   │       └── bobapp/        # Package principal de l'application
│   │   ├── main/resources/        # Ressources de configuration
│   │   │   ├── application.properties  # Configuration Spring Boot
│   │   │   └── json/jokes.json    # Données de blagues
│   │   └── test/java/             # Tests unitaires
│   ├── target/                    # Fichiers générés lors de la compilation
│   ├── Dockerfile                 # Configuration Docker pour le backend
│   ├── pom.xml                    # Configuration Maven et dépendances
│   ├── mvnw                       # Maven Wrapper (Linux/Mac)
│   └── mvnw.cmd                   # Maven Wrapper (Windows)
├── front/                         # Frontend Angular
│   ├── src/
│   │   ├── app/                   # Composants Angular
│   │   │   ├── model/             # Modèles de données TypeScript
│   │   │   ├── services/          # Services Angular
│   │   │   ├── app.component.*    # Composant principal
│   │   │   └── app.module.ts      # Module principal Angular
│   │   ├── assets/                # Ressources statiques
│   │   ├── environments/          # Configuration par environnement
│   │   ├── index.html             # Page HTML principale
│   │   ├── main.ts                # Point d'entrée Angular
│   │   ├── styles.scss            # Styles globaux
│   │   └── test.ts                # Configuration des tests
│   ├── coverage/                  # Rapports de couverture de code
│   ├── Dockerfile                 # Configuration Docker pour le frontend
│   ├── nginx.conf                 # Configuration du serveur web Nginx
│   ├── package.json               # Dépendances et scripts Node.js
│   ├── angular.json               # Configuration Angular CLI
│   ├── karma.conf.js              # Configuration des tests Karma
│   └── tsconfig.json              # Configuration TypeScript
├── .github/workflows/             # Pipelines GitHub Actions
│   ├── ci.yml                     # Pipeline principal CI/CD
│   └── deploy.yml                 # Pipeline de déploiement manuel
├── docker-compose.yml             # Orchestration Docker multi-conteneurs
├── .env.example                   # Exemple de variables d'environnement
├── .gitignore                     # Fichiers ignorés par Git
├── README.md                      # Documentation principale
├── ANALYSE_CI_CD.md              # Documentation d'analyse CI/CD
└── KPI_QUALITY_GATES.md          # Documentation des indicateurs de qualité
```

## Installation et Lancement

### Prérequis

- **Java 17** ou supérieur
- **Node.js 18** ou supérieur
- **Maven 3.6** ou supérieur
- **Docker** (optionnel, pour le déploiement)

### Installation du Projet

1. **Cloner le repository** :
   ```bash
   git clone https://github.com/NairodP/bobapp-ci-cd.git
   cd bobapp-ci-cd
   ```

### Backend (Spring Boot)

1. **Naviguer vers le dossier backend** :

   ```bash
   cd back
   ```

2. **Installer les dépendances** :

   ```bash
   mvn clean install
   ```

3. **Lancer l'application** :

   ```bash
   mvn spring-boot:run
   ```

4. **Lancer les tests** :

   ```bash
   mvn test
   ```

5. **Générer le rapport de couverture** :

   ```bash
   mvn jacoco:report
   ```

   Le rapport sera disponible dans `target/site/jacoco/index.html`

6. **Construire l'image Docker** :

   ```bash
   docker build -t bobapp-back .
   ```

7. **Démarrer le conteneur** :
   ```bash
   docker run -p 8080:8080 --name bobapp-back -d bobapp-back
   ```

**API disponible sur** : http://localhost:8080

### Frontend (Angular)

1. **Naviguer vers le dossier frontend** :

   ```bash
   cd front
   ```

2. **Installer les dépendances** :

   ```bash
   npm install
   ```

3. **Lancer l'application en mode développement** :

   ```bash
   npm start
   ```

4. **Lancer les tests** :

   ```bash
   npm test
   ```

5. **Lancer les tests avec couverture** :

   ```bash
   npm run test -- --code-coverage --watch=false --browsers=ChromeHeadless
   ```

   Le rapport sera disponible dans `coverage/bobapp/index.html`

6. **Construire pour la production** :

   ```bash
   npm run build
   ```

7. **Construire l'image Docker** :

   ```bash
   docker build -t bobapp-front .
   ```

8. **Démarrer le conteneur** :
   ```bash
   docker run -p 80:80 --name bobapp-front -d bobapp-front
   ```

**Application disponible sur** : http://localhost:4200 (dev) ou http://localhost:80 (Docker)

## Déploiement avec Docker Compose

### Configuration

1. **Copier le fichier d'environnement** :

   ```bash
   cp .env.example .env
   ```

2. **Éditer le fichier `.env`** avec vos identifiants Docker Hub :
   ```bash
   DOCKER_USERNAME=votre-username
   DOCKER_PASSWORD=votre-password
   ```

### Lancement

**Démarrer tous les services** :

```bash
docker-compose up -d
```

**Arrêter tous les services** :

```bash
docker-compose down
```

**Voir les logs** :

```bash
docker-compose logs -f
```

## Pipeline CI/CD

### Configuration GitHub Actions

**Secrets requis dans GitHub** :

- `DOCKER_USERNAME` : Nom d'utilisateur Docker Hub
- `DOCKER_PASSWORD` : Mot de passe Docker Hub
- `SONAR_TOKEN` : Token SonarCloud

### Étapes du Pipeline (source : `.github/workflows/ci.yml`)

1. **Tests Backend** :

   - Compilation Maven avec Java 17
   - Exécution des tests JUnit 5
   - Génération du rapport JaCoCo
   - Durée observée : ~30 secondes

2. **Tests Frontend** :

   - Installation des dépendances npm
   - Exécution des tests Karma/Jasmine avec `--code-coverage`
   - Durée observée : ~1 minute

3. **Analyse SonarCloud** :

   - Analyse statique du code (backend + frontend)
   - Vérification du Quality Gate "Sonar way"
   - Durée observée : ~1 minute 30 secondes

4. **Build et Push Docker** :
   - Construction des images backend et frontend
   - Publication automatique sur Docker Hub
   - Durée observée : ~3 minutes

### Déclenchements

- **Automatique** : Push sur la branche `main`
- **Pull Request** : Validation automatique des PR
- **Manuel** : Via l'interface GitHub Actions

## Métriques et Qualité

### Sources des Métriques

- **SonarCloud** : https://sonarcloud.io/organizations/nairodp/projects
- **GitHub Actions** : Onglet Actions du repository pour les temps d'exécution
- **JaCoCo** : Rapports générés dans `target/site/jacoco/`
- **Karma Coverage** : Configuration dans `karma.conf.js`

### KPI et Quality Gates (sources vérifiées)

**Couverture de Code** :

- Nouveau code : ≥ 80% (configuration SonarCloud par défaut)
- Mesure Backend : JaCoCo via `mvn test` puis `mvn jacoco:report`
- Mesure Frontend : Karma Coverage via `npm run test -- --code-coverage`

**Quality Gate SonarCloud** (configuration "Sonar way" par défaut) :

- Issues Blocker : 0
- Issues Critical : 0
- Security Hotspots : 100% reviewed
- Duplication sur nouveau code : ≤ 3%
- Maintainability Rating : A

### Comment Consulter les Métriques

**SonarCloud** :

1. Aller sur https://sonarcloud.io/organizations/nairodp
2. Sélectionner le projet "bobapp-ci-cd"
3. Consulter l'onglet "Overall Code" pour l'état global

**GitHub Actions** :

1. Aller dans l'onglet "Actions" du repository
2. Sélectionner un workflow pour voir les détails et durées
3. Consulter les logs pour les rapports de tests

**Rapports Locaux** :

- Backend : Ouvrir `target/site/jacoco/index.html` après `mvn jacoco:report`
- Frontend : Ouvrir `coverage/bobapp/index.html` après les tests avec `--code-coverage`

## Documentation Technique

- **[Analyse CI/CD Complète](./ANALYSE_CI_CD.md)** : Analyse détaillée du pipeline avec retours utilisateurs et recommandations
- **[KPI et Quality Gates](./KPI_QUALITY_GATES.md)** : Indicateurs de performance, sources et configuration

## Bénéfices du CI/CD pour BobApp

**Pour la Maintenance** :

- Détection automatique des problèmes en quelques minutes
- Déploiement sûr : impossible de déployer du code cassé
- Historique complet et traçabilité de tous les changements

**Pour l'Équipe** :

- Déploiements automatisés et fiables (moins de stress)
- Plus de temps pour développer des features (moins de debugging)
- Confiance grâce aux tests automatiques et quality gates

**Pour les Utilisateurs** :

- Moins de bugs grâce à la validation automatique
- Correctifs plus rapides via le pipeline automatisé
- Livraison plus fréquente et sûre des nouvelles fonctionnalités

## Technologies Utilisées

**Backend** :

- Java 17
- Spring Boot 2.6.1
- Maven
- JUnit 5
- JaCoCo (couverture de code)

**Frontend** :

- Angular 14
- TypeScript
- Karma/Jasmine (tests)
- Node.js 18

**DevOps** :

- GitHub Actions
- Docker & Docker Compose
- SonarCloud
- Docker Hub
