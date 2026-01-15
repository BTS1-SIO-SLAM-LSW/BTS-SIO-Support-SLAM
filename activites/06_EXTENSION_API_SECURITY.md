# EXTENSION API SECURITY
## Ã‰LÃˆVES AVANCÃ‰S SLAM
### Audit de sÃ©curitÃ© des API REST + ConformitÃ© rÃ©glementaire

**BinÃ´me : _________________________ | Date : _______________**

---

> ðŸŽ¯ **Ce document complÃ¨te la cartographie standard.** Vous devez d'abord avoir terminÃ© l'analyse du code et de l'infrastructure. Cette extension analyse :
> 1. Les risques spÃ©cifiques aux **API REST**
> 2. La conformitÃ© aux **rÃ©glementations europÃ©ennes** (NIS2, DORA, RGPD)
> 3. Les **indicateurs de rÃ©silience** (RTO/RPO)

---

# PARTIE 1 : SÃ‰CURITÃ‰ DES API

## Contexte : Pourquoi les API sont une cible privilÃ©giÃ©e

Les API REST sont le principal vecteur d'attaque moderne car :
- Elles exposent directement la **logique mÃ©tier**
- Elles traitent des **donnÃ©es sensibles**
- Elles sont souvent **moins protÃ©gÃ©es** que les interfaces web
- Les outils d'**automatisation** facilitent leur exploitation

## OWASP API Security Top 10 (2023)

| # | Risque | Description | Lien SLAM |
|---|--------|-------------|-----------|
| **API1** | Broken Object Level Authorization | AccÃ¨s Ã  des objets non autorisÃ©s (IDOR) | Composant L + P |
| **API2** | Broken Authentication | Failles d'authentification | Composant L + H |
| **API3** | Broken Object Property Level Auth | AccÃ¨s Ã  des propriÃ©tÃ©s non autorisÃ©es | Composant L |
| **API4** | Unrestricted Resource Consumption | Pas de rate limiting | Composant L + M |
| **API5** | Broken Function Level Authorization | AccÃ¨s Ã  des fonctions admin | Composant L + P |
| **API6** | Unrestricted Access to Business Flows | Abus de logique mÃ©tier | Composant L |
| **API7** | Server Side Request Forgery (SSRF) | RequÃªtes forgÃ©es cÃ´tÃ© serveur | Composant L + M |
| **API8** | Security Misconfiguration | Mauvaise configuration | Composant P |
| **API9** | Improper Inventory Management | API non documentÃ©es | Composant P + D |
| **API10** | Unsafe Consumption of APIs | Consommation non sÃ©curisÃ©e d'API tierces | Supply chain |

---

## Inventaire des endpoints DevSecure

Ã€ partir du code source (app.js), complÃ©tez l'inventaire :

| MÃ©thode | Endpoint | Description | Auth | SPOF ? |
|---------|----------|-------------|------|--------|
| POST | /api/auth/login | Connexion | Non | |
| POST | /api/auth/register | Inscription | Non | |
| GET | /api/projects | Liste projets | Oui | |
| GET | /api/projects/:id | DÃ©tail projet | Oui | |
| GET | /api/projects?q= | Recherche | Oui | |
| | | | | |
| | | | | |

---

## Analyse des vulnÃ©rabilitÃ©s API

### API1 â€” Broken Object Level Authorization (IDOR)

**Question** : Un utilisateur peut-il accÃ©der aux projets d'un autre utilisateur ?

```javascript
// Code DevSecure - getProject
const project = await Project.findOne(JSON.parse(query));
// âš ï¸ VÃ©rifie-t-on que l'utilisateur a le droit d'accÃ©der Ã  ce projet ?
```

| VulnÃ©rabilitÃ© | V | I | Risque | Correction proposÃ©e |
|---------------|---|---|--------|---------------------|
| | | | | |

### API4 â€” Unrestricted Resource Consumption

**Question** : Y a-t-il un rate limiting ?

```javascript
// app.js - Aucun rate limiting visible
app.use(express.json({ limit: '50mb' }));  // Limite trÃ¨s Ã©levÃ©e
```

| VulnÃ©rabilitÃ© | V | I | Risque | Correction proposÃ©e |
|---------------|---|---|--------|---------------------|
| | | | | |

### API8 â€” Security Misconfiguration

**Checklist de configuration** :

| CritÃ¨re | Ã‰tat | VulnÃ©rabilitÃ© ? |
|---------|------|-----------------|
| CORS restrictif | `app.use(cors())` = tout autorisÃ© | â˜ Oui â˜ Non |
| Headers de sÃ©curitÃ© (Helmet.js) | Non mentionnÃ© | â˜ Oui â˜ Non |
| HTTPS forcÃ© | Non vÃ©rifiÃ© | â˜ Oui â˜ Non |
| Messages d'erreur gÃ©nÃ©riques | Stack trace exposÃ©e | â˜ Oui â˜ Non |
| Validation des entrÃ©es | Non visible | â˜ Oui â˜ Non |

---

# PARTIE 2 : CONFORMITÃ‰ RÃ‰GLEMENTAIRE

## Cadre rÃ©glementaire europÃ©en

### NIS2 â€” Network and Information Security Directive 2 (2024)

| Exigence NIS2 | Ã‰tat DevSecure | Conforme ? |
|---------------|----------------|------------|
| Analyse de risques documentÃ©e | Inexistante | â˜ Oui â˜ Non |
| Notification incident sous 24h | Pas de procÃ©dure | â˜ Oui â˜ Non |
| Tests de rÃ©silience rÃ©guliers | Jamais rÃ©alisÃ©s | â˜ Oui â˜ Non |
| Gestion des accÃ¨s et identitÃ©s | Mots de passe partagÃ©s | â˜ Oui â˜ Non |
| SÃ©curitÃ© de la chaÃ®ne d'approvisionnement | Non Ã©valuÃ©e | â˜ Oui â˜ Non |
| Formation cybersÃ©curitÃ© | Inexistante | â˜ Oui â˜ Non |

**DevSecure est-elle concernÃ©e par NIS2 ?**
- [ ] Oui, entitÃ© essentielle
- [ ] Oui, entitÃ© importante
- [ ] Non, mais bonnes pratiques applicables

### DORA â€” Digital Operational Resilience Act (2025)

| Exigence DORA | Application DevSecure |
|---------------|----------------------|
| Tests de pÃ©nÃ©tration avancÃ©s | Non applicable (pas secteur financier) |
| Gestion des risques ICT | Applicable comme bonne pratique |
| Gestion des prestataires tiers | GitHub, AWS, MongoDB = Ã  Ã©valuer |

### RGPD â€” RÃ¨glement GÃ©nÃ©ral sur la Protection des DonnÃ©es (2018)

| Exigence RGPD | Ã‰tat DevSecure | Conforme ? | Risque |
|---------------|----------------|------------|--------|
| DPO dÃ©signÃ© | Non | â˜ Oui â˜ Non | |
| Registre des traitements | Non mentionnÃ© | â˜ Oui â˜ Non | |
| SÃ©curitÃ© des donnÃ©es (art. 32) | Mots de passe en clair | â˜ Oui â˜ Non | |
| Notification violation (72h) | Pas de procÃ©dure | â˜ Oui â˜ Non | |
| Privacy by Design | Non appliquÃ© | â˜ Oui â˜ Non | |

**Sanctions RGPD potentielles** :
- Jusqu'Ã  20 Mâ‚¬ ou 4% du CA mondial
- Pour DevSecure (CA 450 Kâ‚¬) : jusqu'Ã  **18 000 â‚¬** (4%)

---

# PARTIE 3 : ANALYSE DE RÃ‰SILIENCE APPROFONDIE

## Les 4 piliers de la rÃ©silience â€” Analyse dÃ©taillÃ©e

### Pilier 1 : ANTICIPER

| Action | Ã‰tat DevSecure | Recommandation |
|--------|----------------|----------------|
| Analyse de risques formalisÃ©e | âŒ Inexistante | RÃ©aliser une analyse EBIOS |
| Tests de sÃ©curitÃ© (SAST/DAST) | âŒ Jamais rÃ©alisÃ©s | IntÃ©grer dans CI/CD |
| Veille vulnÃ©rabilitÃ©s | âŒ Non faite | Configurer Dependabot |
| `npm audit` rÃ©gulier | âŒ Jamais exÃ©cutÃ© | Automatiser dans pipeline |

### Pilier 2 : RÃ‰SISTER

| Action | Ã‰tat DevSecure | Recommandation |
|--------|----------------|----------------|
| WAF applicatif | âš ï¸ CloudFlare basique | Configurer rÃ¨gles avancÃ©es |
| Rate limiting | âŒ Absent | ImplÃ©menter express-rate-limit |
| Validation des entrÃ©es | âŒ Absente | Utiliser Joi/Yup |
| Segmentation rÃ©seau | âš ï¸ Non Ã©valuÃ©e | Isoler les services |

### Pilier 3 : ABSORBER

| Action | Ã‰tat DevSecure | Recommandation |
|--------|----------------|----------------|
| Mode dÃ©gradÃ© | âŒ Inexistant | DÃ©finir fonctions essentielles |
| Feature flags | âŒ Non utilisÃ©s | ImplÃ©menter LaunchDarkly |
| Circuit breaker | âŒ Absent | Utiliser pattern circuit breaker |
| Failover automatique | âŒ Absent | Configurer multi-rÃ©gion |

### Pilier 4 : SE RÃ‰TABLIR

| Action | Ã‰tat DevSecure | Recommandation |
|--------|----------------|----------------|
| PRA documentÃ© | âŒ Inexistant | RÃ©diger et tester |
| Sauvegardes testÃ©es | âŒ Jamais testÃ©es | Test mensuel de restauration |
| Rollback automatique | âš ï¸ Manuel par Thomas | Automatiser dans CI/CD |
| Communication de crise | âŒ Pas de procÃ©dure | DÃ©finir responsables et messages |

## DÃ©finition des RTO/RPO pour DevSecure

### Analyse des besoins mÃ©tier

| Service | CriticitÃ© | RTO recommandÃ© | RPO recommandÃ© |
|---------|-----------|----------------|----------------|
| Authentification | CRITIQUE | 30 min | 0 (aucune perte) |
| Gestion projets | Ã‰LEVÃ‰E | 2h | 15 min |
| Upload fichiers | MODÃ‰RÃ‰E | 4h | 1h |
| Commentaires | FAIBLE | 8h | 4h |

### Proposition RTO/RPO global

| Indicateur | Valeur actuelle | Valeur proposÃ©e | Actions nÃ©cessaires |
|------------|-----------------|-----------------|---------------------|
| **RTO** | Non dÃ©fini (~infini) | **2 heures** | |
| **RPO** | ~24h (backup quotidien) | **15 minutes** | |

**Actions pour atteindre ces objectifs :**

1. Pour RTO = 2h : _________________________________________________

2. Pour RPO = 15 min : _________________________________________________

---

# PARTIE 4 : SCÃ‰NARIOS D'ATTAQUE

## ScÃ©nario 1 : Exfiltration de donnÃ©es via IDOR + API

**ChaÃ®ne d'attaque** :
1. Attaquant crÃ©e un compte lÃ©gitime
2. RÃ©cupÃ¨re son token JWT
3. Ã‰numÃ¨re les IDs de projets (`/api/projects/1`, `/api/projects/2`...)
4. RÃ©cupÃ¨re TOUS les projets de TOUS les clients

**Impact** :
- Fuite donnÃ©es de 85 clients (2000 utilisateurs)
- Violation RGPD â†’ notification CNIL sous 72h
- Sanction potentielle : jusqu'Ã  18 000 â‚¬

**Composants Laudon impactÃ©s** : â˜ M â˜ L â˜ D â˜ P â˜ H

---

## ScÃ©nario 2 : Ransomware via dÃ©pendance compromise

**ChaÃ®ne d'attaque** (type Log4Shell) :
1. Une des 147 dÃ©pendances npm contient une faille
2. Attaquant exploite la faille via l'API
3. RCE (Remote Code Execution) sur les serveurs
4. Chiffrement de MongoDB et S3

**Impact** :
- ArrÃªt total de l'activitÃ©
- RTO actuel = infini (pas de PRA)
- RPO actuel = 24h de donnÃ©es perdues
- SPOF activÃ© : Thomas seul peut tenter une restauration

**Composants Laudon impactÃ©s** : â˜ M â˜ L â˜ D â˜ P â˜ H

---

# SYNTHÃˆSE EXÃ‰CUTIVE

RÃ©digez un paragraphe (10-15 lignes) **Ã  destination du CEO de DevSecure**, expliquant :
1. Les 3 risques majeurs identifiÃ©s
2. Les obligations rÃ©glementaires non respectÃ©es
3. Les 3 actions prioritaires avec leur coÃ»t estimÃ©

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

# RECOMMANDATIONS PRIORISÃ‰ES

## Urgence immÃ©diate (< 1 semaine)

| Action | Effort | CoÃ»t | Impact |
|--------|--------|------|--------|
| | | | |
| | | | |

## Court terme (< 1 mois)

| Action | Effort | CoÃ»t | Impact |
|--------|--------|------|--------|
| | | | |
| | | | |

## Moyen terme (< 3 mois)

| Action | Effort | CoÃ»t | Impact |
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

*Document Ã©tudiant SLAM â€” Extension avancÃ©e â€” SÃ©ance 1 â€” BTS SIO Bloc 3*
