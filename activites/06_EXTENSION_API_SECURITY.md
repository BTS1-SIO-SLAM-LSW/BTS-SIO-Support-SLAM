# EXTENSION API SECURITY
## ÉLÈVES AVANCÉS SLAM
### Audit de sécurité des API REST + Conformité réglementaire

**Binôme : _________________________ | Date : _______________**

---

> 🎯 **Ce document complète la cartographie standard.** Vous devez d'abord avoir terminé l'analyse du code et de l'infrastructure. Cette extension analyse :
> 1. Les risques spécifiques aux **API REST**
> 2. La conformité aux **réglementations européennes** (NIS2, DORA, RGPD)
> 3. Les **indicateurs de résilience** (RTO/RPO)

---

# PARTIE 1 : SÉCURITÉ DES API

## Contexte : Pourquoi les API sont une cible privilégiée

Les API REST sont le principal vecteur d'attaque moderne car :
- Elles exposent directement la **logique métier**
- Elles traitent des **données sensibles**
- Elles sont souvent **moins protégées** que les interfaces web
- Les outils d'**automatisation** facilitent leur exploitation

## OWASP API Security Top 10 (2023)

| # | Risque | Description | Lien SLAM |
|---|--------|-------------|-----------|
| **API1** | Broken Object Level Authorization | Accès à des objets non autorisés (IDOR) | Composant L + P |
| **API2** | Broken Authentication | Failles d'authentification | Composant L + H |
| **API3** | Broken Object Property Level Auth | Accès à des propriétés non autorisées | Composant L |
| **API4** | Unrestricted Resource Consumption | Pas de rate limiting | Composant L + M |
| **API5** | Broken Function Level Authorization | Accès à des fonctions admin | Composant L + P |
| **API6** | Unrestricted Access to Business Flows | Abus de logique métier | Composant L |
| **API7** | Server Side Request Forgery (SSRF) | Requêtes forgées côté serveur | Composant L + M |
| **API8** | Security Misconfiguration | Mauvaise configuration | Composant P |
| **API9** | Improper Inventory Management | API non documentées | Composant P + D |
| **API10** | Unsafe Consumption of APIs | Consommation non sécurisée d'API tierces | Supply chain |

---

## Inventaire des endpoints DevSecure

À partir du code source (app.js), complétez l'inventaire :

| Méthode | Endpoint | Description | Auth | SPOF ? |
|---------|----------|-------------|------|--------|
| POST | /api/auth/login | Connexion | Non | |
| POST | /api/auth/register | Inscription | Non | |
| GET | /api/projects | Liste projets | Oui | |
| GET | /api/projects/:id | Détail projet | Oui | |
| GET | /api/projects?q= | Recherche | Oui | |
| | | | | |
| | | | | |

---

## Analyse des vulnérabilités API

### API1 — Broken Object Level Authorization (IDOR)

**Question** : Un utilisateur peut-il accéder aux projets d'un autre utilisateur ?

```javascript
// Code DevSecure - getProject
const project = await Project.findOne(JSON.parse(query));
// ⚠️ Vérifie-t-on que l'utilisateur a le droit d'accéder à ce projet ?
```

| Vulnérabilité | V | I | Risque | Correction proposée |
|---------------|---|---|--------|---------------------|
| | | | | |

### API4 — Unrestricted Resource Consumption

**Question** : Y a-t-il un rate limiting ?

```javascript
// app.js - Aucun rate limiting visible
app.use(express.json({ limit: '50mb' }));  // Limite très élevée
```

| Vulnérabilité | V | I | Risque | Correction proposée |
|---------------|---|---|--------|---------------------|
| | | | | |

### API8 — Security Misconfiguration

**Checklist de configuration** :

| Critère | État | Vulnérabilité ? |
|---------|------|-----------------|
| CORS restrictif | `app.use(cors())` = tout autorisé | ☐ Oui ☐ Non |
| Headers de sécurité (Helmet.js) | Non mentionné | ☐ Oui ☐ Non |
| HTTPS forcé | Non vérifié | ☐ Oui ☐ Non |
| Messages d'erreur génériques | Stack trace exposée | ☐ Oui ☐ Non |
| Validation des entrées | Non visible | ☐ Oui ☐ Non |

---

# PARTIE 2 : CONFORMITÉ RÉGLEMENTAIRE

## Cadre réglementaire européen

### NIS2 — Network and Information Security Directive 2 (2024)

| Exigence NIS2 | État DevSecure | Conforme ? |
|---------------|----------------|------------|
| Analyse de risques documentée | Inexistante | ☐ Oui ☐ Non |
| Notification incident sous 24h | Pas de procédure | ☐ Oui ☐ Non |
| Tests de résilience réguliers | Jamais réalisés | ☐ Oui ☐ Non |
| Gestion des accès et identités | Mots de passe partagés | ☐ Oui ☐ Non |
| Sécurité de la chaîne d'approvisionnement | Non évaluée | ☐ Oui ☐ Non |
| Formation cybersécurité | Inexistante | â˜ Oui â˜ Non |

**DevSecure est-elle concernée par NIS2 ?**
- [ ] Oui, entité essentielle
- [ ] Oui, entité importante
- [ ] Non, mais bonnes pratiques applicables

### DORA — Digital Operational Resilience Act (2025)

| Exigence DORA | Application DevSecure |
|---------------|----------------------|
| Tests de pénétration avancés | Non applicable (pas secteur financier) |
| Gestion des risques ICT | Applicable comme bonne pratique |
| Gestion des prestataires tiers | GitHub, AWS, MongoDB = à évaluer |

### RGPD — Règlement Général sur la Protection des Données (2018)

| Exigence RGPD | État DevSecure | Conforme ? | Risque |
|---------------|----------------|------------|--------|
| DPO désigné | Non | ☐ Oui ☐ Non | |
| Registre des traitements | Non mentionné | ☐ Oui ☐ Non | |
| Sécurité des données (art. 32) | Mots de passe en clair | ☐ Oui ☐ Non | |
| Notification violation (72h) | Pas de procédure | ☐ Oui ☐ Non | |
| Privacy by Design | Non appliqué | ☐ Oui ☐ Non | |

**Sanctions RGPD potentielles** :
- Jusqu'à 20 M€ ou 4% du CA mondial
- Pour DevSecure (CA 450 K€) : jusqu'à **18 000 €** (4%)

---

# PARTIE 3 : ANALYSE DE RÉSILIENCE APPROFONDIE

## Les 4 piliers de la résilience — Analyse détaillée

### Pilier 1 : ANTICIPER

| Action | État DevSecure | Recommandation |
|--------|----------------|----------------|
| Analyse de risques formalisée | ❌ Inexistante | Réaliser une analyse EBIOS |
| Tests de sécurité (SAST/DAST) | ❌ Jamais réalisés | Intégrer dans CI/CD |
| Veille vulnérabilités | ❌ Non faite | Configurer Dependabot |
| `npm audit` régulier | ❌ Jamais exécuté | Automatiser dans pipeline |

### Pilier 2 : RÉSISTER

| Action | État DevSecure | Recommandation |
|--------|----------------|----------------|
| WAF applicatif | ⚠️ CloudFlare basique | Configurer règles avancées |
| Rate limiting | ❌ Absent | Implémenter express-rate-limit |
| Validation des entrées | ❌ Absente | Utiliser Joi/Yup |
| Segmentation réseau | ⚠️ Non évaluée | Isoler les services |

### Pilier 3 : ABSORBER

| Action | État DevSecure | Recommandation |
|--------|----------------|----------------|
| Mode dégradé | ❌ Inexistant | Définir fonctions essentielles |
| Feature flags | ❌ Non utilisés | Implémenter LaunchDarkly |
| Circuit breaker | ❌ Absent | Utiliser pattern circuit breaker |
| Failover automatique | ❌ Absent | Configurer multi-région |

### Pilier 4 : SE RÉTABLIR

| Action | État DevSecure | Recommandation |
|--------|----------------|----------------|
| PRA documenté | ❌ Inexistant | Rédiger et tester |
| Sauvegardes testées | ❌ Jamais testées | Test mensuel de restauration |
| Rollback automatique | ⚠️ Manuel par Thomas | Automatiser dans CI/CD |
| Communication de crise | ❌ Pas de procédure | Définir responsables et messages |

## Définition des RTO/RPO pour DevSecure

### Analyse des besoins métier

| Service | Criticité | RTO recommandé | RPO recommandé |
|---------|-----------|----------------|----------------|
| Authentification | CRITIQUE | 30 min | 0 (aucune perte) |
| Gestion projets | ÉLEVÉE | 2h | 15 min |
| Upload fichiers | MODÉRÉE | 4h | 1h |
| Commentaires | FAIBLE | 8h | 4h |

### Proposition RTO/RPO global

| Indicateur | Valeur actuelle | Valeur proposée | Actions nécessaires |
|------------|-----------------|-----------------|---------------------|
| **RTO** | Non défini (~infini) | **2 heures** | |
| **RPO** | ~24h (backup quotidien) | **15 minutes** | |

**Actions pour atteindre ces objectifs :**

1. Pour RTO = 2h : _________________________________________________

2. Pour RPO = 15 min : _________________________________________________

---

# PARTIE 4 : SCÉNARIOS D'ATTAQUE

## Scénario 1 : Exfiltration de données via IDOR + API

**Chaîne d'attaque** :
1. Attaquant crée un compte légitime
2. Récupère son token JWT
3. Énumère les IDs de projets (`/api/projects/1`, `/api/projects/2`...)
4. Récupère TOUS les projets de TOUS les clients

**Impact** :
- Fuite données de 85 clients (2000 utilisateurs)
- Violation RGPD → notification CNIL sous 72h
- Sanction potentielle : jusqu'À  18 000 â‚¬

**Composants Laudon impactés** : â˜ M â˜ L â˜ D â˜ P â˜ H

---

## Scénario 2 : Ransomware via dépendance compromise

**Chaîne d'attaque** (type Log4Shell) :
1. Une des 147 dépendances npm contient une faille
2. Attaquant exploite la faille via l'API
3. RCE (Remote Code Execution) sur les serveurs
4. Chiffrement de MongoDB et S3

**Impact** :
- Arrêt total de l'activité
- RTO actuel = infini (pas de PRA)
- RPO actuel = 24h de données perdues
- SPOF activé : Thomas seul peut tenter une restauration

**Composants Laudon impactés** : â˜ M â˜ L â˜ D â˜ P â˜ H

---

# SYNTHÈSE EXÉCUTIVE

Rédigez un paragraphe (10-15 lignes) **à destination du CEO de DevSecure**, expliquant :
1. Les 3 risques majeurs identifiés
2. Les obligations réglementaires non respectées
3. Les 3 actions prioritaires avec leur coût estimé

_________________________________________________________________

_________________________________________________________________

_________________________________________________________________

_________________________________________________________________

_________________________________________________________________

_________________________________________________________________

_________________________________________________________________

_________________________________________________________________

_________________________________________________________________

_________________________________________________________________

---

# RECOMMANDATIONS PRIORISÉES

## Urgence immédiate (< 1 semaine)

| Action | Effort | CoÀ»t | Impact |
|--------|--------|------|--------|
| | | | |
| | | | |

## Court terme (< 1 mois)

| Action | Effort | CoÀ»t | Impact |
|--------|--------|------|--------|
| | | | |
| | | | |

## Moyen terme (< 3 mois)

| Action | Effort | CoÀ»t | Impact |
|--------|--------|------|--------|
| | | | |
| | | | |

---

# RESSOURCES

- **OWASP API Security Top 10** : https://owasp.org/API-Security/
- **NIS2 Directive** : https://eur-lex.europa.eu/eli/dir/2022/2555
- **DORA Regulation** : https://eur-lex.europa.eu/eli/reg/2022/2554
- **RGPD** : https://www.cnil.fr/fr/rgpd-de-quoi-parle-t-on
- **ANSSI** : https://www.ssi.gouv.fr/

---

*Document étudiant SLAM — Extension avancée — Séance 1 — BTS SIO Bloc 3*
