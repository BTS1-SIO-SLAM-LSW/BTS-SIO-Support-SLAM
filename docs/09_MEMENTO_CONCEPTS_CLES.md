# 🧠 Mémento — Concepts clés à connaître

Ce mémento te sert de **fiche de révision rapide** pendant les activités.

---

## 1) Les bases à maîtriser

- **Vulnérabilité** : faiblesse exploitable dans un système
- **Menace** : cause potentielle d’un incident (attaquant, erreur humaine, panne)
- **Risque** : combinaison de la vraisemblance et de l’impact
- **Incident de sécurité** : événement qui compromet confidentialité, intégrité ou disponibilité

**Formule utile :**

`Risque = Vraisemblance × Impact`

### Définitions flash (faciles à retenir)

- **Actif** : ce qui a de la valeur à protéger (données, appli, serveur)
- **Attaque** : action malveillante pour exploiter une faiblesse
- **Exploit** : technique/code utilisé pour déclencher une vulnérabilité
- **Surface d’attaque** : ensemble des points d’entrée attaquables (API, formulaires, ports)
- **Correctif (patch)** : mise à jour qui corrige une faille
- **Faille “zero-day”** : vulnérabilité connue des attaquants avant le correctif
- **MFA** : vérification en plusieurs facteurs (mot de passe + code/appareil)
- **SPOF (Single Point of Failure)** : élément unique dont la panne peut bloquer tout le service
- **Principe du moindre privilège** : donner seulement les droits strictement nécessaires

---

## 2) Triade CIA (objectif de la cybersécurité)

- **Confidentialité** : seules les personnes autorisées accèdent aux données
- **Intégrité** : les données ne sont pas modifiées de manière non autorisée
- **Disponibilité** : les services restent accessibles

---

## 3) Les 5 composants du SI (Laudon)

1. **Matériel** (serveurs, postes, réseau)
2. **Logiciel** (applications, API, dépendances)
3. **Données** (BDD, fichiers, sauvegardes)
4. **Procédures** (déploiement, revues, gestion des accès)
5. **Humain** (développeurs, admins, utilisateurs)

👉 Une bonne analyse de sécurité couvre **les 5 composants**.

---

## 4) OWASP Top 10 (version synthèse)

- **A01** Broken Access Control
- **A02** Cryptographic Failures
- **A03** Injection (SQL, commandes)
- **A04** Insecure Design
- **A05** Security Misconfiguration
- **A06** Vulnerable and Outdated Components
- **A07** Identification and Authentication Failures
- **A08** Software and Data Integrity Failures
- **A09** Security Logging and Monitoring Failures
- **A10** SSRF

👉 En cartographie, chaque faille doit être reliée à une catégorie OWASP.

---

## 5) Authentification vs Autorisation

- **Authentification** : prouver qui je suis (login, MFA)
- **Autorisation** : définir ce que j’ai le droit de faire (rôles, permissions)

Erreur fréquente : authentifier correctement mais mal contrôler les droits.

---

## 6) Secrets et chiffrement

À ne jamais faire :
- mot de passe en clair
- clé API dans le code source
- token dans un dépôt public

Bonnes pratiques :
- stockage des secrets en variables d’environnement / coffre-fort
- hash des mots de passe avec un algorithme adapté
- TLS/HTTPS partout

---

## 7) Bonnes pratiques de code sécurisé

- Valider les entrées (format, longueur, type)
- Utiliser des requêtes paramétrées (anti SQLi)
- Gérer les erreurs sans exposer d’infos sensibles
- Mettre à jour les dépendances
- Appliquer le principe du moindre privilège

---

## 8) Journalisation et supervision

Objectif : détecter, comprendre, réagir.

À tracer au minimum :
- connexions réussies/échouées
- actions sensibles (suppression, changement de rôle, export)
- erreurs critiques

⚠️ Les logs ne doivent pas contenir de secrets.

---

## 9) Priorisation des risques (grille simple)

- **1 à 3** : faible (surveillance)
- **4 à 7** : modéré (planifier)
- **8 à 11** : élevé (corriger rapidement)
- **12 à 16** : critique (action immédiate)

---

## 10) Réflexe méthode pour un TP cybersécurité

1. Identifier l’actif exposé
2. Trouver la vulnérabilité
3. Classer (OWASP + composant SI)
4. Évaluer le risque (V × I)
5. Proposer une mesure corrective réaliste

---

## ✅ Checklist express avant rendu

- [ ] Mes vulnérabilités sont claires et vérifiables
- [ ] Chaque vulnérabilité a une catégorie OWASP
- [ ] Les 5 composants du SI sont couverts
- [ ] Le scoring est cohérent (vraisemblance + impact)
- [ ] Chaque risque a une recommandation concrète
