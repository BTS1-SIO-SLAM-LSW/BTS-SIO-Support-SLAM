# 📚 GUIDE ÉTUDIANT 
## Séance 1 : Cartographier la vulnérabilité

**Durée** : 2 heures  
**Profils** : Accompagné / Standard / Avancé

---

## 🎯 Votre mission

Vous êtes une équipe de **consultants en sécurité**. Une startup **DevSecure** vous confie l'analyse de sécurité de son SI. 

**Votre objectif** : Identifier toutes les vulnérabilités, les évaluer avec la matrice EBIOS, et proposer des priorités de sécurisation.

**Livrables** :
✅ Cartographie des risques (tableau)  
✅ Identification des SPOF (points uniques de défaillance)  
✅ Justification des priorités (RTO/RPO)  

---

## 📖 Concepts clés (5 min de lecture)

### 1️⃣ Les 5 composants du SI (Laudon)

| Lettre | Composant | Dans DevSecure |
|--------|-----------|-----------------|
| **M** | Matériel | Serveurs AWS, bases de données |
| **L** | Logiciel | Code API Node.js, frameworks |
| **D** | Données | MySQL, sessions utilisateur |
| **P** | Procédures | CI/CD, revue de code |
| **H** | Humain | Développeurs, DevOps |

**Votre travail** : Classer chaque vulnérabilité dans ces 5 catégories

### 2️⃣ OWASP Top 10 (les 10 pires failles web)

| Numéro | Faille | Exemple |
|--------|--------|---------|
| A03 | Injection | SQL injection : `'; DROP TABLE users; --` |
| A02 | Crypto Failed | Mot de passe en clair au lieu de hash |
| A01 | Access Control | Accès admin sans vérification |
| A06 | Vulnerable Components | Dépendance log4j version 2.14 (non patchée) |

**Votre travail** : Identifier quelle faille OWASP pour chaque vulnérabilité

### 3️⃣ Matrice EBIOS (évaluer les risques)

```
RISQUE = VRAISEMBLANCE (1-4) × IMPACT (1-4)

V=4 (très probable) × I=4 (grave) = 16 🔴 CRITIQUE (action immédiate)
V=2 (peu probable) × I=2 (léger) = 4 🟢 FAIBLE (surveillance)
```

**Votre travail** : Pour chaque vulnérabilité, estimer V et I, calculer le risque

---

## 🚀 Comment procéder

### Étape 1️⃣ : Lire la description (10 min)

Ouvrez le fichier `02_SI_FICTIF_DEVSECURE.md`

Lisez attentivement la description de DevSecure :
- Architecture de l'application
- Technos utilisées (Node.js, MongoDB, AWS...)
- Extraits de code fournis

**Posez-vous la question** : "Où vois-je des problèmes de sécurité ?"

### Étape 2️⃣ : Utiliser la grille (20 min)

Ouvrez `03_GRILLE_IDENTIFICATION.md`

Remplissez la grille ligne par ligne :

| Vulnérabilité | Laudon | OWASP | Vraisemblance | Impact | Risque |
|---------------|--------|-------|----------------|--------|--------|
| Mot de passe stocké en clair | L (Logiciel) | A02 - Crypto | 4 | 4 | 16 🔴 |
| ... | | | | | |

**Objectifs minimums** :
- Accompagné : 10 vulnérabilités
- Standard : 15 vulnérabilités
- Avancé : 20 vulnérabilités + RTO/RPO

### Étape 3️⃣ : Compléter le template (20 min)

Ouvrez votre template :
- Accompagné : `05_TEMPLATE_ACCOMPAGNE.md`
- Standard : `04_TEMPLATE_CARTOGRAPHIE.md`
- Avancé : `04_TEMPLATE_CARTOGRAPHIE.md` + `06_EXTENSION_API_SECURITY.md`

Transférez vos vulnérabilités dans le tableau final.

**Formule EBIOS** : Risque = V × I

**Couleurs** :
- 🟢 Faible (1-3)
- 🟡 Modéré (4-7)
- 🔴 Élevé (8-11)
- 🔴 Critique (12-16)

### Étape 4️⃣ : Identifier les SPOF (10 min)

**SPOF** = Single Point of Failure = un élément unique qui paralyse tout

**Questions à vous poser** :
- Y a-t-il qu'UNE base de données ? (si elle tombe, tout s'arrête)
- Y a-t-il qu'UN secret JWT ? (si c'est public, tout est compromis)
- Y a-t-il qu'UNE route d'authentification ? (si elle est bugguée, personne ne peut se connecter)

**Identifiez au moins 2-3 SPOF**

### Étape 5️⃣ : Justifier les priorités (optionnel, profils avancés)

**RTO** = Recovery Time Objective = Combien de temps max on peut perdre cette fonction ?
- API critique : RTO = 1h (4h max tolérable)
- Frontend : RTO = 4h (moins critique)

**RPO** = Recovery Point Objective = Combien de données max on peut perdre ?
- Base utilisateur : RPO = 10 min (sauvegarde toutes les 10 min)
- Logs : RPO = 1h (moins critique)

**Proposez RTO/RPO pour les 3 SPOF les plus critiques**

---

## 🎁 Bonus : Identifier les vulnérabilités "cachées"

L'enseignant a volontairement dissimulé 3 vulnérabilités dans la description.

**Exemples de "caché"** :
- "Les logs ne sont jamais supprimés" → Explosion d'espace disque = DoS
- "Le JWT est stocké en localStorage" → XSS peut le voler
- "Les dépendances sont fixed avec `^` en npm" → Maj auto = version non testée

**Défi** : En trouver au moins 1 de plus que ce qu'on attendait !

---

## 📁 Fichiers à consulter

| Fichier | Quand l'ouvrir | Utilité |
|---------|---|---|
| `02_SI_FICTIF_DEVSECURE.md` | Étape 1️⃣ | Cas d'étude à analyser |
| `03_GRILLE_IDENTIFICATION.md` | Étape 2️⃣ | Support d'analyse |
| `04_TEMPLATE_CARTOGRAPHIE.md` | Étape 3️⃣ | Votre livrable (Standard/Avancé) |
| `05_TEMPLATE_ACCOMPAGNE.md` | Étape 3️⃣ | Votre livrable (Accompagné) |
| `06_EXTENSION_API_SECURITY.md` | Bonus | Pour profils avancés |
| `08_SUPPORT_DE_COURS.md` | Doute ? | Tous les concepts expliqués |

---

## ❓ Questions fréquentes

**Q: Comment je sais si c'est une vulnérabilité ?**  
R: Posez-vous : "Est-ce qu'un attaquant peut exploiter ça ?" ou "Est-ce qu'un truc important peut casser ?"

**Q: Je ne sais pas quel est le V ou I ?**  
R: Demandez à l'enseignant OU regardez `08_SUPPORT_DE_COURS.md` pour des exemples

**Q: Qu'est-ce qu'un SPOF ?**  
R: Un truc unique dont dépend tout. Si c'est down, tout l'appli s'effondre.

**Q: Je dois faire le template en ligne ou papier ?**  
R: En ligne, directement dans le fichier Markdown ou Google Sheets que l'enseignant partagera

**Q: Combien de vulnérabilités "minimum" ?**  
R: Accompagné = 10 | Standard = 15 | Avancé = 20

---

## 🎯 Conseils pour réussir

✅ **Lisez la description 2 fois** — la 1ère pour comprendre, la 2e pour identifier  
✅ **Utilisez la grille** — c'est une checklist, pas une prison  
✅ **Calculez V × I** — c'est mathématique, pas subjectif  
✅ **Posez des questions** — il n'y a pas de questions bêtes  
✅ **Pensez comme un attaquant** — "Comment je casserais cette app ?"  
✅ **Cherchez les dépendances** — npm audit c'est ton ami  

---

## 🏆 Évaluation

Vous serez évalué sur :

| Critère | Points | Indicateur |
|---------|--------|------------|
| Nombre de vulnérabilités | /5 | 10+ pour accompagné, 15+ pour standard, 20+ pour avancé |
| Classification Laudon | /5 | 100% des vulnérabilités classées M/L/D/P/H |
| Scoring EBIOS | /5 | Formule V × I correcte, niveaux bien attribués |
| SPOF identifiés | /5 | Au moins 2-3 SPOF pertinents et justifiés |
| RTO/RPO (avancé) | /5 | Justifiés et réalistes |

**Total** : /25 (ou /20 selon profil)

---


Bon courage ! 🚀

---

*Séance 1/4 — Cybersécurité et Résilience Organisationnelle*
