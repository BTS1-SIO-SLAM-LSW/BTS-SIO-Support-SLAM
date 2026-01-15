# GRILLE D'IDENTIFICATION DES VULNÉRABILITÉS
## Version SLAM — Audit applicatif DevSecure

**Binôme : _________________________ | Date : _______________**

---

# RAPPELS THÉORIQUES

## Les 5 composants du SI (Laudon & Laudon)

| Composant | Description | Focus SLAM |
|-----------|-------------|------------|
| **M** - Matériel | Infrastructure physique/cloud | Serveurs AWS, MongoDB Atlas, Redis |
| **L** - Logiciel | Applications et systèmes | **Code applicatif**, frameworks, dÃ©pendances |
| **D** - Données | Informations stockÃ©es | **BDD**, fichiers S3, sauvegardes, logs |
| **P** - Procédures | Règles et processus | **CI/CD**, revue de code, documentation |
| **H** - Personnel | Ressources humaines | **Développeurs**, compÃ©tences sÃ©curitÃ© |

> ðŸ”‘ **Mnémonique** : MLDPP = "**M**a **L**igne **D**e **P**rotection **P**ermanente"

## VulnÃ©rabilitÃ© / Menace / Risque

| Concept | Définition | Caractéristique |
|---------|------------|-----------------|
| **VulnÃ©rabilitÃ©** | Faiblesse du systÃ¨me | Intrinsèque (interne) |
| **Menace** | Ce qui peut exploiter la vulnÃ©rabilitÃ© | Externe |
| **Risque** | ProbabilitÃ©×Impact | Calculable |

```
VULNÃ‰RABILITÃ‰ â†’ exploitÃ©e par â†’ MENACE â†’ cause â†’ IMPACT = RISQUE
```

## Formule du risque (EBIOS)

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚   RISQUE = VRAISEMBLANCE (V)×IMPACT (I)  â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

## OWASP Top 10 â€” 2021 (catÃ©gories principales)

| Code | CatÃ©gorie | Description |
|------|-----------|-------------|
| **A01** | Broken Access Control | AccÃ¨s non autorisÃ© (IDOR) |
| **A02** | Cryptographic Failures | Données non protÃ©gÃ©es |
| **A03** | Injection | SQL, NoSQL, XSS, commandes |
| **A05** | Security Misconfiguration | Mauvaise configuration |
| **A06** | Vulnerable Components | DÃ©pendances obsolÃ¨tes |
| **A07** | Auth Failures | Authentification faible |
| **A09** | Logging Failures | Journalisation insuffisante |

---

# PARTIE 1 : ANALYSE DU CODE â€” VULNÃ‰RABILITÃ‰S APPLICATIVES

## Extrait 1 : auth.controller.js (Authentification)

| # | Ligne(s) | VulnÃ©rabilitÃ© | OWASP | Laudon | Justification |
|---|----------|---------------|-------|--------|---------------|
| C1 | | | | | |
| C2 | | | | | |
| C3 | | | | | |
| C4 | | | | | |

**Questions d'aide :**
- OÃ¹ est stockÃ©e la clÃ© JWT ? Est-ce sÃ©curisÃ© ?
- Comment sont vÃ©rifiÃ©s les mots de passe ?
- Que contiennent les logs en cas d'erreur ?
- Quelle est la durÃ©e de validitÃ© du token ?

---

## Extrait 2 : project.controller.js (Projets)

| # | Ligne(s) | VulnÃ©rabilitÃ© | OWASP | Laudon | Justification |
|---|----------|---------------|-------|--------|---------------|
| C5 | | | | | |
| C6 | | | | | |

**Questions d'aide :**
- Comment est construite la requÃªte MongoDB ?
- Que fait `$where` avec une entrÃ©e utilisateur ?
- Un utilisateur peut-il accÃ©der aux projets d'un autre ?

---

## Extrait 3 : upload.controller.js (Upload)

| # | Ligne(s) | VulnÃ©rabilitÃ© | OWASP | Laudon | Justification |
|---|----------|---------------|-------|--------|---------------|
| C7 | | | | | |
| C8 | | | | | |
| C9 | | | | | |

**Questions d'aide :**
- OÃ¹ sont les clés AWS ? Est-ce sÃ©curisÃ© ?
- Le nom de fichier est-il validÃ© ?
- Quelle est la visibilitÃ© par dÃ©faut des fichiers ?

---

## Extrait 4 : Comments.jsx (Frontend)

| # | Ligne(s) | VulnÃ©rabilitÃ© | OWASP | Laudon | Justification |
|---|----------|---------------|-------|--------|---------------|
| C10 | | | | | |

**Question d'aide :**
- Que signifie `dangerouslySetInnerHTML` ? Pourquoi est-ce dangereux ?

---

## Extrait 5 : app.js (Configuration)

| # | Ligne(s) | VulnÃ©rabilitÃ© | OWASP | Laudon | Justification |
|---|----------|---------------|-------|--------|---------------|
| C11 | | | | | |
| C12 | | | | | |
| C13 | | | | | |

**Questions d'aide :**
- Que fait `cors()` sans paramÃ¨tres ?
- La limite de 50 Mo est-elle raisonnable ?
- Que contient la rÃ©ponse d'erreur en production ?

---

# PARTIE 2 : ANALYSE INFRASTRUCTURE â€” 5 COMPOSANTS LAUDON

## Composant M â€” MATÃ‰RIEL / CLOUD

| # | VulnÃ©rabilitÃ© | Menace associÃ©e | Justification |
|---|---------------|-----------------|---------------|
| M1 | | | |
| M2 | | | |
| M3 | | | |

**Questions d'aide :**
- Y a-t-il une redondance sur MongoDB Atlas ?
- Que se passe-t-il si Redis tombe ?
- L'infrastructure est-elle mono-rÃ©gion ?

---

## Composant L â€” LOGICIEL (hors code applicatif)

| # | VulnÃ©rabilitÃ© | Menace associÃ©e | Justification |
|---|---------------|-----------------|---------------|
| L1 | | | |
| L2 | | | |
| L3 | | | |

**Questions d'aide :**
- Quelle version de Node.js est utilisÃ©e ?
- Depuis combien de temps les dÃ©pendances npm n'ont pas Ã©tÃ© mises Ã  jour ?
- `npm audit` a-t-il Ã©tÃ© exÃ©cutÃ© ?

---

## Composant D â€” DONNÃ‰ES

| # | VulnÃ©rabilitÃ© | Menace associÃ©e | Justification |
|---|---------------|-----------------|---------------|
| D1 | | | |
| D2 | | | |
| D3 | | | |

**Questions d'aide :**
- Comment sont stockÃ©s les mots de passe ?
- Les sauvegardes sont-elles testÃ©es ?
- Quelle est la perte de donnÃ©es maximale en cas d'incident (RPO) ?

---

## Composant P â€” PROCÃ‰DURES / DEVOPS

| # | VulnÃ©rabilitÃ© | Menace associÃ©e | Justification |
|---|---------------|-----------------|---------------|
| P1 | | | |
| P2 | | | |
| P3 | | | |
| P4 | | | |

**Questions d'aide :**
- Y a-t-il une revue de code systÃ©matique ?
- Existe-t-il un environnement de staging ?
- Comment sont partagÃ©s les secrets (clés API) ?
- Existe-t-il un plan de reprise d'activitÃ© (PRA) ?

---

## Composant H â€” PERSONNEL

| # | VulnÃ©rabilitÃ© | Menace associÃ©e | Justification |
|---|---------------|-----------------|---------------|
| H1 | | | |
| H2 | | | |
| H3 | | | |

**Questions d'aide :**
- Le personnel est-il formÃ© Ã  la cybersÃ©curitÃ© ?
- Y a-t-il une personne unique qui dÃ©tient des connaissances critiques ?
- La direction est-elle impliquÃ©e dans la sÃ©curitÃ© ?

---

# PARTIE 3 : IDENTIFICATION DES SPOF

> **SPOF** = Single Point of Failure = Point unique de dÃ©faillance
> 
> Question clÃ© : Â« **Si cet Ã©lÃ©ment tombe, que se passe-t-il ?** Â»

## SPOF identifiÃ©s

| # | Type | Ã‰lÃ©ment | Impact si dÃ©faillance | Solution proposÃ©e |
|---|------|---------|----------------------|-------------------|
| SPOF1 | | | | |
| SPOF2 | | | | |
| SPOF3 | | | | |
| SPOF4 | | | | |
| SPOF5 | | | | |

**Types de SPOF Ã  rechercher :**
- ðŸ–¥ï¸ **Matériel** : Serveur/service unique
- ðŸ’¿ **Logiciel** : DÃ©pendance critique unique
- ðŸ“Š **Données** : Sauvegarde unique ou non testÃ©e
- ðŸ‘¤ **Humain** : Personne unique indispensable
- ðŸ“‹ **ProcÃ©dure** : Processus unique sans alternative

---

# PARTIE 4 : ANALYSE DE RÃ‰SILIENCE

## RTO et RPO actuels de DevSecure

| Indicateur | Valeur actuelle | Valeur recommandÃ©e | Ã‰cart |
|------------|-----------------|-------------------|-------|
| **RTO** (temps max d'interruption) | | | |
| **RPO** (perte de donnÃ©es max) | | | |

## Les 4 piliers de la rÃ©silience â€” Ã‰tat DevSecure

| Pilier | Ã‰tat (âŒ/âš ï¸/âœ…) | Justification |
|--------|----------------|---------------|
| **Anticiper** | | |
| **RÃ©sister** | | |
| **Absorber** | | |
| **Se rÃ©tablir** | | |

---

# SYNTHÃˆSE

## Comptage par catÃ©gorie

| CatÃ©gorie | Nombre |
|-----------|--------|
| **VulnÃ©rabilitÃ©s CODE (OWASP)** | |
| A01 - Broken Access Control | |
| A02 - Cryptographic Failures | |
| A03 - Injection | |
| A05 - Security Misconfiguration | |
| A06 - Vulnerable Components | |
| A07 - Auth Failures | |
| A09 - Logging Failures | |
| **VulnÃ©rabilitÃ©s INFRA (Laudon)** | |
| M - Matériel | |
| L - Logiciel | |
| D - Données | |
| P - Procédures | |
| H - Personnel | |
| **SPOF identifiÃ©s** | |
| **TOTAL VULNÃ‰RABILITÃ‰S** | |

---

## Top 5 des vulnÃ©rabilitÃ©s les plus critiques

| Rang | RÃ©f. | VulnÃ©rabilitÃ© | OWASP | Laudon | Impact |
|------|------|---------------|-------|--------|--------|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |
| 4 | | | | | |
| 5 | | | | | |

---

# QUESTIONS DE RÃ‰FLEXION

## 1. ChaÃ®ne d'attaque

DÃ©crivez un scÃ©nario combinant plusieurs vulnÃ©rabilitÃ©s :

_________________________________________________________________

_________________________________________________________________

_________________________________________________________________

## 2. SPOF le plus critique

Quel SPOF aurait l'impact le plus grave et pourquoi ?

_________________________________________________________________

_________________________________________________________________

## 3. Quick wins

Quelles sont les 3 corrections les plus simples Ã  implÃ©menter ?

1. _________________________________________________________________

2. _________________________________________________________________

3. _________________________________________________________________

---

*Document Ã©tudiant SLAM â€” SÃ©ance 1 â€” BTS SIO Bloc 3*
