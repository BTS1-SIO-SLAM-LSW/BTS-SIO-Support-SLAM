# 🔐 Support en Cybersécurité — Parcours étudiant 
## Cartographier les vulnérabilités d'une application

![Version](https://img.shields.io/badge/version-1.0-blue)
![Niveau](https://img.shields.io/badge/niveau-1ère%20année-blue)
![Durée](https://img.shields.io/badge/durée-2h-yellow)
![Mode](https://img.shields.io/badge/mode-100%25%20en%20ligne-brightgreen)

---

## 👋 Bienvenue !

Tu vas apprendre à **identifier et analyser les vulnérabilités d'une application web**.

Cette séance va te montrer comment les hackers trouvent les failles, et surtout **comment toi, tu les identifies en tant que développeur**.

**Durée totale** : 2 heures  
**Groupe** : Binôme (2 personnes)  
**Résultat final** : Une cartographie des risques (à soumettre sur GitHub)

---

## 🗺️ TON PARCOURS EN 4 PHASES

### Phase 1️⃣ : Comprendre (15 min)

**Objectif** : Voir un vrai incident de sécurité

```
📺 Regarder vidéo : Log4Shell incident (YouTube, ~5 min)
   ↓
🎯 Questions à te poser :
   □ Comment le hacker a exploité la faille ?
   □ Quels systèmes ont été touchés ?
   □ Pourquoi c'était si grave ?
```

✅ **Validation** : Tu comprends qu'une faille logicielle peut paralyser le monde entier

---

### Phase 2️⃣ : Analyser (45 min)

**Objectif** : Analyser une application fictive

```
📄 Lire le document : 02_SI_FICTIF_DEVSECURE.md
   ↓
📋 Ouvrir la grille : 03_GRILLE_IDENTIFICATION.md
   ↓
🔍 Trouver les vulnérabilités :
   □ Lire le code (oui, du vrai code !)
   □ Repérer les failles
   □ Classer avec OWASP Top 10
   □ Noter chaque risque identifié
```

**DevSecure** = Une startup SaaS (comme Slack ou Stripe)

```
Qu'est-ce qu'on analyse ?
├─ 🖥️ Serveurs (infrastructure)
├─ 💾 Bases de données (données sensibles)
├─ 🔌 API (comment on la contacte)
├─ 👨‍💻 Code (les vrais bugs)
└─ 👤 Utilisateurs (comment ils l'utilisent)
```

**Exemple de vulnérabilités à trouver :**
- Injection SQL (A03) : Entrer du code dans un formulaire
- Secrets en dur (A02) : Clés d'accès visibles dans le code
- Pas HTTPS (A02) : Les données peuvent être lues en route
- Dépendances outdated (A06) : Log4j vulnerable (comme Log4Shell)

✅ **Validation** : Tu as identifié au moins 12 vulnérabilités

---

### Phase 3️⃣ : Cartographier (45 min)

**Objectif** : Créer une matrice de risques

```
📊 Ouvrir le template : 04_TEMPLATE_CARTOGRAPHIE.md
   ↓
📝 Remplir pour chaque vulnérabilité :
   □ Nom
   □ Composant (SLAM: Logiciel/Données/Procédures/Humain/Matériel)
   □ Catégorie OWASP
   □ Vraisemblance (1-4) : Facile à exploiter ?
   □ Impact (1-4) : Grave si exploitée ?
   □ RISQUE = V × I (scoring)
   □ Niveau (Faible/Modéré/Élevé/Critique)
```

**Comment scorer ?**

```
Vraisemblance (V) :
🟢 1 = Très difficile à exploiter
🟡 2 = Difficile
🟠 3 = Facile
🔴 4 = Très facile (visible)

Impact (I) :
🟢 1 = Petits dégâts
🟡 2 = Dégâts moyens
🟠 3 = Gros dégâts
🔴 4 = Catastrophe (données perdues, service down)

RISQUE = V × I :
🟢 1-3 = Surveiller
🟡 4-7 = Action dans 3-6 mois
🟠 8-11 = Action dans 1 mois
🔴 12-16 = ACTION IMMÉDIATE
```

**Exemple :**
```
Injection SQL
├─ Vraisemblance : 4 (très facile, entrée pas validée)
├─ Impact : 4 (on peut lire/modifier toutes les données)
├─ RISQUE : 4 × 4 = 16 (CRITIQUE !)
└─ Solution : Utiliser requêtes paramétrées
```

✅ **Validation** : Matrice complète, tous les 5 composants couverts, scoring justifié

---

### Phase 4️⃣ : Mettre en commun (15 min)

**Objectif** : Comparer et apprendre

```
👨‍🏫 Enseignant montre 2-3 exemples
   ↓
💬 Discussion : Pourquoi vos scores diffèrent ?
   ↓
🔍 Démo live : Injection SQL en vraie
   (Tu vois comment on rentre du code dans un formulaire)
   ↓
📌 Leçons clés révélées
```

✅ **Validation** : Tu comprends les solutions (secure code, tests, monitoring)

---

## 📚 LES CONCEPTS CLÉ

### LAUDON — 5 composants du SI

Quand on analyse une application, on la regarde sous 5 angles :

```
🖥️ MATÉRIEL
   = Serveurs, cloud, conteneurs
   Exemple de risque : Serveur surchargé (pas de scalabilité)

💾 LOGICIEL
   = Code, frameworks, librairies
   Exemple de risque : Injection SQL (bug dans le code)

📊 DONNÉES
   = Bases de données, fichiers, sessions
   Exemple de risque : Mots de passe en clair

⚙️ PROCÉDURES
   = Comment on fait le code (CI/CD, tests, revue)
   Exemple de risque : Pas de tests de sécurité

👥 HUMAIN
   = Développeurs, DevOps, utilisateurs
   Exemple de risque : Développeur ne connaît pas la sécurité
```

**Dans le TP :** Tu dois identifier au moins 1-2 failles par composant

---

### OWASP Top 10 — Les 10 failles applicatives les plus graves

```
A01 | Broken Access Control
     → On accède à quelque chose sans permission (admin panel visible)

A02 | Cryptographic Failures
     → Les données ne sont pas protégées (mots de passe en clair, pas HTTPS)

A03 | INJECTION (SQL, Command)
     → On rentre du code dans un formulaire
     → SELECT * FROM users WHERE id = 1 OR 1=1 --

A04 | Insecure Design
     → L'archi est mal pensée (API sans auth)

A05 | Security Misconfiguration
     → Mal configuré (debug mode actif, fichiers publics)

A06 | Vulnerable Components
     → On utilise des dépendances outdated
     → Exemple : log4j vulnerable (Log4Shell)

A07 | Identification Failures
     → Faible authentification (mot de passe facile)

A08 | Data Integrity Failures
     → Les données peuvent être modifiées en route (MITM)

A09 | Logging Failures
     → Pas de traçabilité (on sait pas qui a fait quoi)

A10 | SSRF
     → On force l'app à accéder à des resources internes
```

**Dans le TP :** Tu vas classer tes vulnérabilités par catégorie OWASP

---

### EBIOS — Analyser les risques

C'est une **méthode française officiellement recommandée**.

```
Etape 1 : Identifier les vulnérabilités
          ↓
Etape 2 : Évaluer la vraisemblance (V)
          "Facile à exploiter ?"
          ↓
Etape 3 : Évaluer l'impact (I)
          "Grave si exploitée ?"
          ↓
Etape 4 : Calculer le RISQUE
          RISQUE = V × I
          ↓
Etape 5 : Prioriser les actions
          (Traiter les critiques d'abord)
```

**C'est l'outil que tu vas utiliser dans le TP**

---

## 🎯 CE QUE TU DOIS FAIRE

### ✅ AVANT LA SÉANCE (si tu as le temps)

```
□ Lire : 02_SI_FICTIF_DEVSECURE.md (15 min)
  → Comprendre ce qu'est DevSecure
  
□ Consulter : 03_GRILLE_IDENTIFICATION.md (5 min)
  → Voir le format attendu
  
□ (Optionnel) Lire : 08_SUPPORT_DE_COURS.md (20 min)
  → Apprendre les concepts OWASP
```

### 📌 PENDANT LA SÉANCE

```
⏱️ 0-15 min  : Regarder vidéo + discussion
⏱️ 15-60 min : Analyser DevSecure + remplir grille
⏱️ 60-105 min: Créer cartographie EBIOS (binôme)
⏱️ 105-120 min: Synthèse + démo
```

**Ton deliverable** = Fichier `.md` avec la matrice des risques

### 📤 APRÈS LA SÉANCE (remise sur GitHub)

Consulte la section **🔧 GITHUB — REMISE DE TON TRAVAIL** ci-dessous

---

## 📚 RESSOURCES

### Pendant la séance
- 📄 02_SI_FICTIF_DEVSECURE.md → La vraie app à analyser
- 📋 03_GRILLE_IDENTIFICATION.md → Le format
- 📝 04_TEMPLATE_CARTOGRAPHIE.md → Ton template
- 🧠 docs/09_MEMENTO_CONCEPTS_CLES.md → Fiche de révision rapide

### Pour apprendre plus
- 📖 08_SUPPORT_DE_COURS.md → Tous les concepts
- 🎬 YouTube "Log4Shell vulnerability" (~5 min)
- 🌐 https://owasp.org/www-project-top-ten/

### Après la séance
- ✅ 07_CORRIGE_COMPLET.md → La solution (enseignant la partagera)

---

## 🔧 GITHUB — REMISE DE TON TRAVAIL

**Tu dois remettre ta cartographie sur GitHub** (c'est un outil professionnel que tu vas utiliser en industrie !)

### 📌 AVANT LA SÉANCE (15 min)

**Livrable 0️⃣ : Vérifier que tu as compris les concepts**

👉 Lis et complète : **`LIVRABLE_0_CONCEPTS_GITHUB.md`**

```
✅ 4 exercices simples (15 minutes)
✅ Vérifier que tu comprends GitHub/Markdown
✅ À envoyer par e-mail AVANT le TP
✅ Pas noté, juste une vérification
```

**Contenu** :
- Définitions (GitHub, dépôt, commit, etc.)
- Associations fonctions GitHub
- Markdown pratique
- Cas d'usage réel

**À faire** :
1. Télécharge le fichier
2. Remplis les 4 exercices
3. Envoie tes réponses par e-mail

---

### 📖 PENDANT LA SÉANCE (référence)

**Guide 📖 : Tout ce qu'il faut savoir sur GitHub**

👉 Consulte : **`GUIDE_GITHUB_ETUDIANT.md`**

```
✅ 4 concepts clés expliqués simplement
✅ 12 fonctions GitHub essentielles
✅ 4 usages courants
✅ 5 commandes Git de base
✅ 3 outils pour mettre en forme (VS Code, Mistral, Dillinger)
✅ Workflow complet Word → GitHub
✅ Markdown cheatsheet
✅ Auto-évaluation pour vérifier
✅ Dépannage (6 problèmes courants)
```

**Comment l'utiliser** :
- Avant de commencer : lis les concepts
- Pendant le TP : garde-le ouvert comme référence
- Besoin d'aide ? Cherche dans le dépannage

---

### 🚀 APRÈS LA SÉANCE (remise)

**Étapes pour remettre ton travail** :

```
1️⃣ Créer un compte GitHub (gratuit)
   → https://github.com/signup
   → Username : prenom_nom_bts

2️⃣ Créer un dépôt
   → Bouton "+" → "New repository"
   → Nom : TP_DevSecure_Cartographie
   → Public (très important !)

3️⃣ Uploader ta cartographie
   → "Add file" → "Upload files"
   → Sélectionne ton fichier Markdown
   → "Commit changes"

4️⃣ Envoyer l'URL à l'enseignant
   → https://github.com/ton_username/TP_DevSecure_Cartographie
```

**Temps total** : 10 minutes maximum

---

### 📋 FORMAT DE TON FICHIER À REMETTRE

Ton fichier Markdown doit contenir :

```markdown
# Cartographie des risques — DevSecure

## 👥 Binôme
- Étudiant 1 : [Nom]
- Étudiant 2 : [Nom]

## 🔍 Vulnérabilités identifiées

| Vulnérabilité | Composant | OWASP | V | I | Risque | Niveau |
|---|---|---|---|---|---|---|
| Injection SQL | Software | A03 | 4 | 4 | 16 | 🔴 CRITIQUE |
| Secret JWT en dur | Software | A02 | 4 | 3 | 12 | 🔴 CRITIQUE |
| [Ajouter les autres] | | | | | | |

## 💪 Points forts
- [Qu'est-ce qui est bien dans DevSecure ?]

## ⚠️ Points à améliorer
- [Qu'est-ce qui pose problème ?]

## 🎯 Solutions proposées
- [Comment corriger les failles ?]
```

✅ **Important** : Fichier en format `.md` (Markdown), pas Word !

---

### 🛠️ OUTILS POUR METTRE EN FORME (optionnel)

Si tu veux voir ton travail bien formaté **avant d'uploader** :

| Outil | Utilité | Lien |
|---|---|---|
| **VS Code** | Éditeur avec aperçu temps réel | https://code.visualstudio.com |
| **Mistral** | IA qui formate ton texte en Markdown | https://mistral.ai/chat |
| **Dillinger** | Testeur Markdown en ligne | https://dillinger.io |

✨ **Conseil** : Utilise Mistral si tu as du texte à formatter rapidement !

---

### ❓ QUESTIONS FRÉQUENTES

**Q: C'est compliqué GitHub ?**  
**R:** Non ! Juste "Add file" → "Upload" → "Commit". Tu vas comprendre naturellement.

**Q: Je dois avoir un compte avant la séance ?**  
**R:** Idéal, mais pas obligatoire. Tu peux le créer après aussi.

**Q: Comment je sais si mon fichier est au bon format ?**  
**R:** Une fois uploadé, GitHub te montre le rendu. Si c'est lisible = c'est bon !

**Q: Vous allez corriger sur GitHub aussi ?**  
**R:** Oui ! L'enseignant laissera des commentaires directement sur ton fichier.

---

## 🚀 TON OBJECTIF

### À la fin de cette séance, tu dois pouvoir :

```
✅ Identifier les vulnérabilités d'une application
   (au moins 12-15)

✅ Les classer par catégorie OWASP Top 10
   (A01-A10)

✅ Scorer chaque risque avec EBIOS
   (V × I)

✅ Justifier pourquoi une faille est grave
   (impact métier)

✅ Proposer des solutions
   (code sécurisé, tests, monitoring)

✅ Comprendre le lien entre code et sécurité
   (tu feras de la cybersécurité en tant que dev)

✅ Utiliser GitHub comme un pro
   (créer dépôt, uploader, recevoir feedback)
```

---

## 💡 CONSEILS PRATIQUES

### Pour trouver les vulnérabilités

```
1️⃣ Lire le code (vraiment !)
   → Chercher les patterns dangereux

2️⃣ Utiliser la checklist OWASP
   → Penser à chaque catégorie (A01-A10)

3️⃣ Se demander : "Et si je suis un hacker ?"
   → Comment j'exploite ça ?

4️⃣ Analyser chaque composant Laudon
   → Matériel, Logiciel, Données, Procédures, Humain

5️⃣ Évaluer VRAIMENT (pas random)
   → V : Combien de temps pour exploiter ?
   → I : Quel dégât si exploitée ?
```

### Pour scorer correctement

```
V = Vraisemblance (V)
   ↳ Si c'est visible/facile → 3-4
   ↳ Si c'est caché → 1-2

I = Impact (I)
   ↳ Si c'est juste un warning → 1-2
   ↳ Si on perd des données → 4

RISQUE = V × I
   ↳ 16 = CRITIQUE (c'est mon boss qui appelle !)
   ↳ 12 = Grave (fix rapidement)
   ↳ 6-8 = Moyen (dans le sprint)
   ↳ 2-4 = Faible (backlog)
```

---

## 🎓 COMPÉTENCES QUE TU DÉVELOPPES

Pendant cette séance, tu travailles sur :

**Concevoir une solution applicative sécurisée**
- ✅ Participer à la conception de l'architecture
- ✅ Adapter des composants sécurisés

**Cybersécurité d'une application**
- ✅ Vérifier la qualité du développement
- ✅ Prendre en compte la sécurité du code
- ✅ Mettre en œuvre des standards (OWASP)
- ✅ Prévenir les attaques
- ✅ Analyser les incidents et proposer des solutions

**Travail en équipe**
- ✅ Collaborer en binôme
- ✅ Soumettre sur GitHub (outil professionnel)

---

## ✅ CHECKLIST FINAL (À cocher au fur et à mesure)

### Phase 1 : Comprendre
- [ ] J'ai regardé la vidéo Log4Shell
- [ ] Je comprends pourquoi c'est grave
- [ ] Je sais qu'un bug logiciel peut avoir des conséquences énormes

### Phase 2 : Analyser
- [ ] J'ai lu DevSecure.md
- [ ] J'ai lu la grille OWASP
- [ ] J'ai identifié au moins 12 vulnérabilités
- [ ] Elles sont classées par OWASP

### Phase 3 : Cartographier
- [ ] J'ai créé ma matrice EBIOS
- [ ] Tous les 5 composants Laudon sont couverts
- [ ] J'ai scoré (V × I)
- [ ] J'ai proposé des solutions

### Phase 4 : Remise GitHub
- [ ] J'ai complété le Livrable 0 (concepts)
- [ ] J'ai lu le Guide GitHub
- [ ] J'ai créé un compte GitHub
- [ ] J'ai créé un dépôt
- [ ] J'ai uploadé ma cartographie
- [ ] J'ai envoyé l'URL à l'enseignant

### Résultat
- [ ] Fichier bien formé
- [ ] Toutes les vulnérabilités listées
- [ ] Scoring justifié
- [ ] Solutions proposées
- [ ] En ligne sur GitHub

---

## 🎉 ÇA Y EST !

Félicitations ! Tu viens de :
- ✅ Analyser une app comme un pentester
- ✅ Utiliser une méthode pro (EBIOS)
- ✅ Justifier la sécurité avec des chiffres
- ✅ Soumettre sur GitHub (vrai outil pro)
- ✅ Construire un portfolio
- ✅ Maîtriser les concepts de GitHub

**Continue comme ça. La sécurité, c'est l'avenir.** 🚀

---

## 📜 Licence

CC-BY-NC-SA — Libre pour usage pédagogique

---

**Créé le** : Janvier 2025  
**Intégration GitHub** : 2 guides étudiants + 1 livrable de vérification  
**BTS SIO — Bloc 3 — Compétence C1**
