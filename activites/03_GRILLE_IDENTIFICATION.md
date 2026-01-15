# GRILLE D'IDENTIFICATION DES VULNÀRABILITÀS
## Version SLAM â Audit applicatif DevSecure

**BinÀ´me : _________________________ | Date : _______________**

---

# RAPPELS THÀORIQUES

## Les 5 composants du SI (Laudon & Laudon)

| Composant | Description | Focus SLAM |
|-----------|-------------|------------|
| **M** - Matériel | Infrastructure physique/cloud | Serveurs AWS, MongoDB Atlas, Redis |
| **L** - Logiciel | Applications et systèmes | **Code applicatif**, frameworks, dÀÂ©pendances |
| **D** - Données | Informations stockÀÂ©es | **BDD**, fichiers S3, sauvegardes, logs |
| **P** - Procédures | Règles et processus | **CI/CD**, revue de code, documentation |
| **H** - Personnel | Ressources humaines | **Développeurs**, compÀÂ©tences sÀÂ©curitÀÂ© |

> À°Å¸ââ **Mnémonique** : MLDPP = "**M**a **L**igne **D**e **P**rotection **P**ermanente"

## VulnÀÂ©rabilitÀÂ© / Menace / Risque

| Concept | Définition | Caractéristique |
|---------|------------|-----------------|
| **VulnÀÂ©rabilitÀÂ©** | Faiblesse du systÀÂ¨me | Intrinsèque (interne) |
| **Menace** | Ce qui peut exploiter la vulnÀÂ©rabilitÀÂ© | Externe |
| **Risque** | ProbabilitÀÂ©ÀImpact | Calculable |

```
VULNÀâ°RABILITÀâ° À¢â â exploitÀÂ©e par À¢â â MENACE À¢â â cause À¢â â IMPACT = RISQUE
```

## Formule du risque (EBIOS)

```
À¢âÅÀ¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢âÂ
À¢ââ   RISQUE = VRAISEMBLANCE (V)ÀIMPACT (I)  À¢ââ
À¢ââÀ¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢ââ¬À¢âË
```

## OWASP Top 10 À¢â¬â 2021 (catÀÂ©gories principales)

| Code | CatÀÂ©gorie | Description |
|------|-----------|-------------|
| **A01** | Broken Access Control | AccÀÂ¨s non autorisÀÂ© (IDOR) |
| **A02** | Cryptographic Failures | Données non protÀÂ©gÀÂ©es |
| **A03** | Injection | SQL, NoSQL, XSS, commandes |
| **A05** | Security Misconfiguration | Mauvaise configuration |
| **A06** | Vulnerable Components | DÀÂ©pendances obsolÀÂ¨tes |
| **A07** | Auth Failures | Authentification faible |
| **A09** | Logging Failures | Journalisation insuffisante |

---

# PARTIE 1 : ANALYSE DU CODE À¢â¬â VULNÀâ°RABILITÀâ°S APPLICATIVES

## Extrait 1 : auth.controller.js (Authentification)

| # | Ligne(s) | VulnÀÂ©rabilitÀÂ© | OWASP | Laudon | Justification |
|---|----------|---------------|-------|--------|---------------|
| C1 | | | | | |
| C2 | | | | | |
| C3 | | | | | |
| C4 | | | | | |

**Questions d'aide :**
- OÀÂ¹ est stockÀÂ©e la clÀÂ© JWT ? Est-ce sÀÂ©curisÀÂ© ?
- Comment sont vÀÂ©rifiÀÂ©s les mots de passe ?
- Que contiennent les logs en cas d'erreur ?
- Quelle est la durÀÂ©e de validitÀÂ© du token ?

---

## Extrait 2 : project.controller.js (Projets)

| # | Ligne(s) | VulnÀÂ©rabilitÀÂ© | OWASP | Laudon | Justification |
|---|----------|---------------|-------|--------|---------------|
| C5 | | | | | |
| C6 | | | | | |

**Questions d'aide :**
- Comment est construite la requÀÂªte MongoDB ?
- Que fait `$where` avec une entrÀÂ©e utilisateur ?
- Un utilisateur peut-il accÀÂ©der aux projets d'un autre ?

---

## Extrait 3 : upload.controller.js (Upload)

| # | Ligne(s) | VulnÀÂ©rabilitÀÂ© | OWASP | Laudon | Justification |
|---|----------|---------------|-------|--------|---------------|
| C7 | | | | | |
| C8 | | | | | |
| C9 | | | | | |

**Questions d'aide :**
- OÀÂ¹ sont les clés AWS ? Est-ce sÀÂ©curisÀÂ© ?
- Le nom de fichier est-il validÀÂ© ?
- Quelle est la visibilitÀÂ© par dÀÂ©faut des fichiers ?

---

## Extrait 4 : Comments.jsx (Frontend)

| # | Ligne(s) | VulnÀÂ©rabilitÀÂ© | OWASP | Laudon | Justification |
|---|----------|---------------|-------|--------|---------------|
| C10 | | | | | |

**Question d'aide :**
- Que signifie `dangerouslySetInnerHTML` ? Pourquoi est-ce dangereux ?

---

## Extrait 5 : app.js (Configuration)

| # | Ligne(s) | VulnÀÂ©rabilitÀÂ© | OWASP | Laudon | Justification |
|---|----------|---------------|-------|--------|---------------|
| C11 | | | | | |
| C12 | | | | | |
| C13 | | | | | |

**Questions d'aide :**
- Que fait `cors()` sans paramÀÂ¨tres ?
- La limite de 50 Mo est-elle raisonnable ?
- Que contient la rÀÂ©ponse d'erreur en production ?

---

# PARTIE 2 : ANALYSE INFRASTRUCTURE À¢â¬â 5 COMPOSANTS LAUDON

## Composant M À¢â¬â MATÀâ°RIEL / CLOUD

| # | VulnÀÂ©rabilitÀÂ© | Menace associÀÂ©e | Justification |
|---|---------------|-----------------|---------------|
| M1 | | | |
| M2 | | | |
| M3 | | | |

**Questions d'aide :**
- Y a-t-il une redondance sur MongoDB Atlas ?
- Que se passe-t-il si Redis tombe ?
- L'infrastructure est-elle mono-rÀÂ©gion ?

---

## Composant L À¢â¬â LOGICIEL (hors code applicatif)

| # | VulnÀÂ©rabilitÀÂ© | Menace associÀÂ©e | Justification |
|---|---------------|-----------------|---------------|
| L1 | | | |
| L2 | | | |
| L3 | | | |

**Questions d'aide :**
- Quelle version de Node.js est utilisÀÂ©e ?
- Depuis combien de temps les dÀÂ©pendances npm n'ont pas ÀÂ©tÀÂ© mises ÀÂ  jour ?
- `npm audit` a-t-il ÀÂ©tÀÂ© exÀÂ©cutÀÂ© ?

---

## Composant D À¢â¬â DONNÀâ°ES

| # | VulnÀÂ©rabilitÀÂ© | Menace associÀÂ©e | Justification |
|---|---------------|-----------------|---------------|
| D1 | | | |
| D2 | | | |
| D3 | | | |

**Questions d'aide :**
- Comment sont stockÀÂ©s les mots de passe ?
- Les sauvegardes sont-elles testÀÂ©es ?
- Quelle est la perte de donnÀÂ©es maximale en cas d'incident (RPO) ?

---

## Composant P À¢â¬â PROCÀâ°DURES / DEVOPS

| # | VulnÀÂ©rabilitÀÂ© | Menace associÀÂ©e | Justification |
|---|---------------|-----------------|---------------|
| P1 | | | |
| P2 | | | |
| P3 | | | |
| P4 | | | |

**Questions d'aide :**
- Y a-t-il une revue de code systÀÂ©matique ?
- Existe-t-il un environnement de staging ?
- Comment sont partagÀÂ©s les secrets (clés API) ?
- Existe-t-il un plan de reprise d'activitÀÂ© (PRA) ?

---

## Composant H À¢â¬â PERSONNEL

| # | VulnÀÂ©rabilitÀÂ© | Menace associÀÂ©e | Justification |
|---|---------------|-----------------|---------------|
| H1 | | | |
| H2 | | | |
| H3 | | | |

**Questions d'aide :**
- Le personnel est-il formÀÂ© ÀÂ  la cybersÀÂ©curitÀÂ© ?
- Y a-t-il une personne unique qui dÀÂ©tient des connaissances critiques ?
- La direction est-elle impliquÀÂ©e dans la sÀÂ©curitÀÂ© ?

---

# PARTIE 3 : IDENTIFICATION DES SPOF

> **SPOF** = Single Point of Failure = Point unique de dÀÂ©faillance
> 
> Question clÀÂ© : À« **Si cet ÀÂ©lÀÂ©ment tombe, que se passe-t-il ?** À»

## SPOF identifiÀÂ©s

| # | Type | Àâ°lÀÂ©ment | Impact si dÀÂ©faillance | Solution proposÀÂ©e |
|---|------|---------|----------------------|-------------------|
| SPOF1 | | | | |
| SPOF2 | | | | |
| SPOF3 | | | | |
| SPOF4 | | | | |
| SPOF5 | | | | |

**Types de SPOF ÀÂ  rechercher :**
- À°Å¸âÂ¥À¯Â¸Â **Matériel** : Serveur/service unique
- À°Å¸âÂ¿ **Logiciel** : DÀÂ©pendance critique unique
- À°Å¸âÅ  **Données** : Sauvegarde unique ou non testÀÂ©e
- À°Å¸âÂ¤ **Humain** : Personne unique indispensable
- À°Å¸ââ¹ **ProcÀÂ©dure** : Processus unique sans alternative

---

# PARTIE 4 : ANALYSE DE RÀâ°SILIENCE

## RTO et RPO actuels de DevSecure

| Indicateur | Valeur actuelle | Valeur recommandÀÂ©e | Àâ°cart |
|------------|-----------------|-------------------|-------|
| **RTO** (temps max d'interruption) | | | |
| **RPO** (perte de donnÀÂ©es max) | | | |

## Les 4 piliers de la rÀÂ©silience À¢â¬â Àâ°tat DevSecure

| Pilier | Àâ°tat (À¢ÂÅ/À¢Å¡Â À¯Â¸Â/À¢Åâ¦) | Justification |
|--------|----------------|---------------|
| **Anticiper** | | |
| **RÀÂ©sister** | | |
| **Absorber** | | |
| **Se rÀÂ©tablir** | | |

---

# SYNTHÀËSE

## Comptage par catÀÂ©gorie

| CatÀÂ©gorie | Nombre |
|-----------|--------|
| **VulnÀÂ©rabilitÀÂ©s CODE (OWASP)** | |
| A01 - Broken Access Control | |
| A02 - Cryptographic Failures | |
| A03 - Injection | |
| A05 - Security Misconfiguration | |
| A06 - Vulnerable Components | |
| A07 - Auth Failures | |
| A09 - Logging Failures | |
| **VulnÀÂ©rabilitÀÂ©s INFRA (Laudon)** | |
| M - Matériel | |
| L - Logiciel | |
| D - Données | |
| P - Procédures | |
| H - Personnel | |
| **SPOF identifiÀÂ©s** | |
| **TOTAL VULNÀâ°RABILITÀâ°S** | |

---

## Top 5 des vulnÀÂ©rabilitÀÂ©s les plus critiques

| Rang | RÀÂ©f. | VulnÀÂ©rabilitÀÂ© | OWASP | Laudon | Impact |
|------|------|---------------|-------|--------|--------|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |
| 4 | | | | | |
| 5 | | | | | |

---

# QUESTIONS DE RÀâ°FLEXION

## 1. ChaÀÂ®ne d'attaque

DÀÂ©crivez un scÀÂ©nario combinant plusieurs vulnÀÂ©rabilitÀÂ©s :

_________________________________________________________________

_________________________________________________________________

_________________________________________________________________

## 2. SPOF le plus critique

Quel SPOF aurait l'impact le plus grave et pourquoi ?

_________________________________________________________________

_________________________________________________________________

## 3. Quick wins

Quelles sont les 3 corrections les plus simples ÀÂ  implÀÂ©menter ?

1. _________________________________________________________________

2. _________________________________________________________________

3. _________________________________________________________________

---

*Document ÀÂ©tudiant SLAM À¢â¬â SÀÂ©ance 1 À¢â¬â BTS SIO Bloc 3*
