# 🔐 BTS SIO Cybersécurité — Option SLAM
## Séance 1 : Cartographier la vulnérabilité

![Version](https://img.shields.io/badge/version-1.0-blue)
![License](https://img.shields.io/badge/license-CC--BY--NC--SA-green)
![Status](https://img.shields.io/badge/status-Prêt%20pour%20déploiement-success)

---

## 📚 À propos

**Ressources pédagogiques complètes** pour enseigner la cybersécurité aux étudiants **BTS SIO Option SLAM** (Solutions Logicielles et Applications Métiers), **1ère année, Bloc 3 - Compétence C1**.

Cette séance introduit l'**analyse de risques informatiques** en mettant l'accent sur les **vulnérabilités applicatives**, le **développement sécurisé** et la **pensée critique** face aux propositions technologiques.

---

## 🎯 Objectifs pédagogiques

À la fin de cette séance, l'étudiant sera capable de :

✅ **Identifier** les vulnérabilités d'une application selon les 5 composants du SI (Laudon)  
✅ **Classer** les failles applicatives selon OWASP Top 10  
✅ **Analyser** les risques avec la méthode EBIOS (Vraisemblance × Impact)  
✅ **Détecter** les points uniques de défaillance (SPOF) critiques  
✅ **Justifier** les priorités de sécurisation (RTO/RPO)  
✅ **Exercer** l'esprit critique face aux propositions de l'IA  

---

## 📁 Structure du répertoire

```
BTS-SIO-Cybersecurite-SLAM/
├── README.md                          ← Ce fichier
├── .gitignore
│
├── docs/                              📖 Documentation théorique
│   ├── 01_FICHE_ENSEIGNANT.md        (Préparation enseignant)
│   ├── 02_SI_FICTIF_DEVSECURE.md     (Cas d'étude : startup SaaS)
│   ├── 08_SUPPORT_DE_COURS.md        (Concepts SLAM complets)
│   └── 09_ACCROCHE_SCENARIO.md       (Log4Shell scenario)
│
├── activites/                         🎯 Travail étudiant
│   ├── 03_GRILLE_IDENTIFICATION.md   (Grille d'analyse)
│   └── 06_EXTENSION_API_SECURITY.md  (Profils avancés)
│
├── templates/                         📋 Livrables
│   ├── 04_TEMPLATE_CARTOGRAPHIE.md   (Standard)
│   └── 05_TEMPLATE_ACCOMPAGNE.md     (Accompagné)
│
└── corrige/                           ✅ Correction
    └── 07_CORRIGE_COMPLET.md         (Solution complète)
```

---

## ⏱️ Déroulement (2h)

| Phase | Durée | Activité | Focus |
|-------|-------|----------|-------|
| **1** | 15 min | Log4Shell incident video | SPOF logiciel, supply chain |
| **2** | 45 min | Analyser DevSecure app | Code, OWASP, dépendances |
| **3** | 45 min | Cartographie des risques | EBIOS matrix |
| **4** | 15 min | Démo SQL injection | Théorie → Réalité |

---

## 📊 Concepts clés SLAM

### Laudon — 5 composants
- **M**atériel : Serveurs cloud, conteneurs
- **L**ogiciel : **Code applicatif**, frameworks, API
- **D**onnées : **Bases de données**, sessions, logs
- **P**rocédures : **CI/CD**, revue de code, tests
- **H**umain : **Développeurs**, DevOps

### OWASP Top 10 — Failles applicatives

| Rang | Catégorie | Exemple |
|------|-----------|---------|
| A01 | Broken Access Control | Accès admin sans vérification |
| A02 | Cryptographic Failures | Données/secrets en clair |
| A03 | Injection | SQL, NoSQL, Command injection |
| A04 | Insecure Design | API sans authentification |
| A05 | Security Misconfiguration | Debug mode, logs verbeux |
| A06 | Vulnerable Components | Dépendances outdated (log4j) |
| A07 | Authentication Failures | Mot de passe faible, pas 2FA |
| A08 | Data Integrity Failures | MITM, signature invalide |
| A09 | Logging & Monitoring | Pas de trace audit |
| A10 | SSRF | Accès interne depuis l'app |

### EBIOS Risk = Vraisemblance (1-4) × Impact (1-4)

```
🟢 Faible (1-3)    | 🟡 Modéré (4-7)  | 🔴 Élevé (8-11)  | 🔴 Critique (12-16)
Surveillance      | 3-6 mois          | 1 mois            | Immédiat
```

---

## 👥 Différenciation

| Profil | Binômes | Objectif | Template |
|--------|---------|----------|----------|
| Accompagné | 3 | ≥ 10 vulnérabilités | Pré-rempli |
| Standard | 6 | ≥ 15 vulnérabilités | Vierge |
| Avancé | 3 | 20 vulnérabilités + RTO/RPO | Vierge + Extension |

---

## ✅ Critères de réussite

- [ ] 80% des binômes : ≥ 12 vulnérabilités
- [ ] 100% : Tous les 5 composants Laudon couverts
- [ ] 100% : Scoring EBIOS correct
- [ ] 50% : Détection vulnérabilité "cachée"

---

## 📚 Ressources

- 🎬 **Log4Shell incident** : YouTube (5 min)
- 📖 **OWASP Top 10** : https://owasp.org/www-project-top-ten/
- 📖 **ANSSI EBIOS** : https://www.anssi.gouv.fr
- 🛠️ **DVWA** : Injection SQL démo (https://github.com/digininja/DVWA)

---

## 🎓 Compétences BTS SIO mobilisées

**Bloc 1 : Concevoir et développer une solution applicative**
- Participer à la conception de l'architecture d'une solution applicative
- Identifier, développer, utiliser ou adapter des composants logiciels

**Bloc 3 : Cybersécurité des services informatiques (SLAM)**
- **Assurer la cybersécurité d'une solution applicative et de son développement**
  - Participer à la vérification des éléments contribuant à la qualité d'un développement informatique
  - Prendre en compte la sécurité dans un projet de développement d'une solution applicative
  - Mettre en œuvre et vérifier la conformité d'une solution applicative à un standard de sécurité
  - Prévenir les attaques
  - Analyser les incidents de sécurité, proposer et mettre en œuvre des contre-mesures

---

## 📜 Licence

CC-BY-NC-SA — Libre pour usage pédagogique  
Mention d'auteur requise, pas d'usage commercial

*Séance 1/4 — Cybersécurité et Résilience — SLAM*
