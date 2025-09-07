# Plateforme IPS - Démo Technique

**Redéploiement live possible en entretien** : Choisissez votre stack technique préférée (Java/Python/.NET + Angular/React) et assistez au déploiement complet en 15 minutes via le pipeline automatisé.

---

Plateforme d'analyse des Indicateurs de Position Sociale des établissements scolaires - Application web de recherche géolocalisée permettant de trouver les établissements (écoles, collèges, lycées) les plus proches d'une adresse donnée avec leurs IPS respectifs.

## Fonctionnalité principale

**Interface de recherche géolocalisée** : 
- Saisie libre d'une adresse
- Sélection du type d'établissement (école, collège, lycée)
- Affichage des résultats triés par proximité croissante
- Visualisation des IPS pour chaque établissement

**Cas d'usage concrets** :
- **Parents** : Recherche d'établissements proches du domicile avec comparaison des IPS
- **Agences immobilières** : Valorisation des biens par proximité d'établissements à IPS élevés
- **Collectivités** : Analyse de la répartition géographique et planification scolaire
- **Chercheurs** : Études des corrélations géographiques et mixité sociale

## Vue d'ensemble technique

Cette plateforme illustre une architecture cloud moderne pour le traitement et la visualisation de données publiques éducatives. Le projet démontre l'implémentation d'une stack complète avec des pratiques **DevOps** solides (CI/CD automatisé, Infrastructure as Code), **DataOps** adaptatif (pipeline dual-mode pour optimisation temporelle), et configuration **SecOps** standard.

## Architecture globale

### Stack technologique multi-frameworks

**Frontend modulaire**
- Angular (TypeScript) - Interface principale
- ReactJS (alternative) - Implémentation React disponible
- Azure Static Web Apps pour l'hébergement (déploiement depuis code source)
- Build optimisé avec cache et CDN global

**Backend polyglotte**
- Java Spring Boot - API REST principale avec actuator
- Python FastAPI - Alternative async haute performance  
- .NET Core - Implémentation C# disponible
- Containerisation Docker pour tous les backends

**Infrastructure Azure**
- App Service pour les conteneurs backend
- Static Web Apps pour le frontend
- Azure Database for PostgreSQL (ou Neon externe)
- Container Registry pour les images Docker
- Key Vault pour la gestion des secrets

## Pipeline CI/CD unifié - Approche DevOps

### Workflow GitHub Actions en 4 phases

**Phase 1: Build Applications (DevOps)**
```
- Détection automatique du type de backend/frontend
- Build conditionnel selon la stack choisie
- Tests unitaires intégrés
- Création d'images Docker optimisées
- Artifacts partagés entre jobs avec versioning sémantique
```

**Phase 2: Deploy Infrastructure (DevOps + SecOps)** 
```
- Terraform pour l'Infrastructure as Code (IaC)
- Validation des paramètres avec fallbacks sécurisés
- Nettoyage automatique de l'environnement
- Provisioning conditionnel avec least privilege principles
- Outputs exposés pour les phases suivantes
```

**Phase 3: Deploy Applications (DevOps + SecOps)**
```
- Push images vers Azure Container Registry sécurisé
- Déploiement App Service avec configuration zero-trust
- Migration base avec Flyway et validation de schéma
- Configuration CORS automatique et sécurisée
- Health checks multi-niveaux et monitoring
```

**Phase 4: Import Data (DataOps - Conditionnel)**
```
- Pipeline de données automatisé avec validation qualité
- Mode Azure: Import complet des données IPS (~1h30)
- Mode externe: Bypass de l'import (base pré-alimentée)
- Monitoring des métriques de données et alerting
- Optimisation pour démonstrations rapides
```

## Détails techniques d'implémentation

### Gestion multi-stack intelligente

Le pipeline détecte et adapte automatiquement la configuration selon les choix :

**Variables dynamiques**
```yaml
BACKEND_TYPE: Java|Python|DotNet
FRONTEND_TYPE: Angular|ReactJs
BASE_EXTERNE: true|false (Neon vs Azure DB)
```

**Chemins calculés**
```yaml
BACKEND_PATH: backend/{type}/etablissements-proximite
Frontend build adaptatif selon le framework
Configuration d'environnement injectée
```

### Infrastructure as Code (Terraform)

**Ressources provisionnées**
- Resource Group avec naming convention
- PostgreSQL flexible server ou configuration externe
- App Service plan Linux avec Docker support
- Static Web App avec custom domains
- Container Registry avec admin access
- Key Vault avec access policies

**Gestion des modes de base (DataOps)**
- Mode Azure: Création PostgreSQL managée + import complet des données (~1h30)
- Mode externe: Utilise une base Neon pré-alimentée pour déploiement rapide (~15 min)
- Validation et fallbacks automatiques selon le mode
- Outputs conditionnels selon la configuration choisie

### Containerisation avancée

**Images Docker sécurisées**
- Utilisateur non-root pour la sécurité (appuser)
- Health checks intégrés dans les conteneurs

**Registry et déploiement**
- Push automatique vers Azure Container Registry
- Tagging avec SHA et latest
- Configuration App Service avec nouvelle image
- Redémarrage App Service pour appliquer les changements

### Base de données et migrations

**Flyway pour les migrations**
- Scripts SQL versionnés (création tables et fonctions)
- Baseline automatique pour nouveaux environnements

**Gestion des connexions sécurisées (SecOps)**
- Variables d'environnement externalisées pour les credentials
- Secrets stockés dans Key Vault (récupérés par le pipeline)

## Monitoring et observabilité

### Health checks et monitoring
```
- Application health endpoint (/actuator/health)
- Health check Docker intégré (30s interval)
- Database connectivity test basique
```

### Logging
```
- GitHub Actions: logs de pipeline standard
- Azure App Service: logs applicatifs Spring Boot avec retention (7 jours)
- Application Insights: monitoring applicatif et métriques
- Log Analytics Workspace pour centralisation
- Logging DEBUG activé (SQL, Web requests)
```

## Sécurité et bonnes pratiques (SecOps)

### Gestion des secrets
- Service Principal Azure pour l'authentification
- Key Vault pour le stockage des mots de passe PostgreSQL
- Variables d'environnement externalisées (pas de secrets hardcodés)

### Réseau et accès
- HTTPS par défaut sur Azure Static Web Apps et App Service
- CORS configuré entre frontend et backend
- Firewall PostgreSQL avec accès restreint (Azure Cloud Shell + IPs spécifiques)

## Architecture technique standard

### Configuration frontend
- Build production Angular avec budgets de taille configurés
- Output hashing pour cache busting (`"outputHashing": "all"`)
- CDN global via Azure Static Web Apps

### Configuration backend
- Configuration PostgreSQL avec driver natif
- Health endpoints Spring Boot Actuator
- Logging détaillé pour debugging (SQL, Web requests)

### Infrastructure Azure
- App Service plan Linux pour containers
- Azure Database for PostgreSQL flexible server
- Container Registry pour les images Docker
- Services managés Azure avec haute disponibilité par défaut

## Choix d'architecture et justifications

### Stratégie de déploiement dual-mode
- **Mode production (Azure)**: Infrastructure complète avec données fraîches
- **Mode démonstration (externe)**: Base pré-alimentée pour déploiements rapides
- **Optimisation temporelle**: 15 min vs 1h30 selon les besoins business
- **DataOps adaptatif**: Pipeline selon le contexte d'usage

### Pourquoi cette stack?
- **Multi-framework**: Démontre la flexibilité d'un pipeline unifié
- **Containerisation**: Portabilité et cohérence des environnements
- **Azure**: Écosystème intégré avec services managés
- **Terraform**: Infrastructure versionnée et reproductible
- **Base externe**: Stratégie de données pré-provisionnées pour l'agilité

### Pattern Pipeline
- **Phases séquentielles**: Validation avant déploiement
- **Artifacts partagés**: Optimisation des builds
- **Conditional logic**: Support multi-configuration
- **Rollback capability**: Nettoyage automatique en cas d'échec

### Données et API
- **PostgreSQL**: Performance pour l'analytique géospatiale
- **REST API**: Standard et facilement intégrable
- **Flyway**: Migrations versionnées
- **OpenData**: Source officielle et actualisée

## Temps de déploiement

### Performance de déploiement
- **Mode Azure complet**: ~1h45 (build 5 min + infra 10 min + données 1h30)
- **Mode externe rapide**: ~15 min (build 5 min + infra 10 min + bypass données)
- **Optimisation démonstration**: Mode externe pour déploiements live en entretien

Cette architecture démontre l'implémentation d'une plateforme fonctionnelle avec des pratiques DevOps solides et une infrastructure Azure standard, dimensionnée pour une démonstration technique efficace.
