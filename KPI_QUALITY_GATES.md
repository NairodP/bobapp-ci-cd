# KPIs et Quality Gates - BobApp

## Introduction

Ce document définit les indicateurs de performance clés (KPIs) et les seuils de qualité (Quality Gates) pour le projet BobApp. Pour une application simple d'affichage de blagues, l'objectif principal est de maintenir un CI/CD fiable qui simplifie la maintenance.

## Sources des Métriques

- **SonarCloud** : Analyse de code automatique via https://sonarcloud.io/organizations/nairodp
- **GitHub Actions** : Pipeline CI/CD visible dans l'onglet Actions du repository
- **JaCoCo** : Rapports de couverture Maven générés automatiquement
- **Karma/Jasmine** : Tests Angular avec rapports de couverture

## KPIs Essentiels

### KPI 1 : Couverture de Code

**Description** : Pourcentage de code couvert par les tests automatisés

**Seuils SonarCloud par défaut** :

- Nouveau code : ≥ 80% (configuration SonarCloud standard)
- Code existant : Pas de seuil imposé (amélioration progressive)

**Justification** :

- Détecter les régressions sur les nouvelles fonctionnalités
- Simplifier la maintenance avec des tests automatisés

**Mesure** :

- Backend : JaCoCo dans le pipeline Maven (`mvn test` puis `mvn jacoco:report`)
- Frontend : Karma Coverage via `npm run test -- --code-coverage` (source : karma.conf.js et ci.yml)

### KPI 2 : Quality Gate SonarCloud

**Description** : Validation automatique de la qualité du code

**Seuils SonarCloud par défaut** :

- Issues Blocker : 0 (configuration par défaut SonarCloud)
- Issues Critical : 0 (configuration par défaut SonarCloud)
- Security Hotspots : 100% reviewed (standard SonarCloud)

**Justification** :

- Prévenir les bugs critiques en production
- Maintenir un code maintenable pour une équipe réduite

**Mesure** : Quality Gate automatique dans le pipeline GitHub Actions

### KPI 3 : Pipeline CI/CD

**Description** : Fiabilité du processus de déploiement automatique

**Mesures observables** :

- Temps d'exécution : Visible dans GitHub Actions
- Taux de succès : Historique dans l'onglet Actions
- Fréquence de déploiement : Logs GitHub Actions

**Justification** :

- Simplifier la maintenance par l'automatisation
- Réduire les erreurs humaines lors des déploiements

## Configuration Actuelle

### SonarCloud Quality Gate

La configuration utilise le Quality Gate par défaut de SonarCloud "Sonar way" :

- Coverage sur nouveau code : ≥ 80%
- Duplication sur nouveau code : ≤ 3%
- Maintainability Rating : A
- Reliability Rating : A
- Security Rating : A

Source : https://sonarcloud.io/organizations/nairodp/quality_gates

### GitHub Actions

Configuration dans `.github/workflows/ci.yml` :

- Tests backend obligatoires
- Tests frontend obligatoires
- SonarCloud Quality Gate obligatoire
- Build Docker conditionnel au succès des étapes précédentes

## Bénéfices pour la Maintenance

### Automatisation

- **Déploiement** : Docker Hub automatique après validation
- **Tests** : Exécution automatique sur chaque modification
- **Qualité** : Analyse SonarCloud systématique

### Simplification

- **Un seul pipeline** : Backend + Frontend + Déploiement
- **Feedback rapide** : Détection des problèmes en quelques minutes
- **Documentation** : Historique visible dans GitHub Actions

### Fiabilité

- **Tests automatisés** : Détection des régressions
- **Quality Gates** : Blocage des modifications problématiques
- **Rollback possible** : Images Docker versionnées

## Comment Consulter les Métriques

### SonarCloud

1. Aller sur https://sonarcloud.io/organizations/nairodp
2. Sélectionner le projet "bobapp-ci-cd"
3. Consulter l'onglet "Overall Code" pour l'état global

### GitHub Actions

1. Aller dans l'onglet "Actions" du repository
2. Sélectionner un workflow pour voir les détails
3. Consulter les logs pour les temps d'exécution

### Rapports de Couverture

- **Backend** : Générés par JaCoCo dans `target/site/jacoco/`
- **Frontend** : Affichés dans les logs du job "test-frontend"

## Conclusion

Ces KPIs se concentrent sur l'essentiel pour BobApp : maintenir un pipeline CI/CD fiable qui simplifie la maintenance d'une application de blagues. Les seuils utilisent les configurations par défaut de SonarCloud, éprouvées et reconnues dans l'industrie.

L'objectif n'est pas la perfection métrique mais la simplification opérationnelle : déployer en confiance avec un feedback rapide sur la qualité.
