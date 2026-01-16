# DESCRIPTION DU SYSTÈME D'INFORMATION
## Startup DevSecure – Plateforme SaaS de gestion de projets

**Document étudiant  – Séance 1**

---

> **Contexte** : Vous êtes développeur sécurité (DevSecOps) en mission d'audit. La startup DevSecure vous a transmis cette description de leur SI et des extraits de code.
>
> **Votre mission** :
> 1. Identifier TOUTES les vulnérabilités (infrastructure ET code)
> 2. Les classer par **composant Laudon** (M, L, D, P, H) et **catégorie OWASP**
> 3. Identifier les **SPOF** (points uniques de défaillance)
> 4. Évaluer les risques avec la **méthode EBIOS** (V × I)

---

# PRÉSENTATION DE L'ENTREPRISE

DevSecure est une startup fondée en 2021, spécialisée dans le développement d'une plateforme SaaS de gestion de projets collaboratifs destinée aux PME. L'équipe est composée de 12 personnes, principalement des développeurs.

| Donnée | Valeur |
|--------|--------|
| **Effectif** | 12 personnes (8 développeurs, 2 commerciaux, 1 CEO, 1 office manager) |
| **Chiffre d'affaires** | 450 K€ (2024) |
| **Clients** | 85 PME (environ 2 000 utilisateurs actifs) |
| **Données hébergées** | Projets, tâches, fichiers, données clients |
| **Locaux** | Espace coworking à Lyon Part-Dieu |
| **Contraintes métier** | Disponibilité 24/7 attendue par les clients |

---

# ARCHITECTURE TECHNIQUE

## Infrastructure

```
┌─────────────────────────────────────────────────────────┐
│                        INTERNET                         │
└────────────────────────┬────────────────────────────────┘
                         │
                    ┌────▼─────┐
                    │ CloudFlare│  (CDN + WAF basique)
                    └────┬─────┘
                         │
             ┌───────────────────────┐
             │  Load Balancer AWS    │
             └───────────┬───────────┘
                         │
        ┌────────────────┼────────────────┐
        │                │                │
   ┌────▼────┐      ┌────▼────┐     ┌────▼────┐
   │ App 1    │      │ App 2    │     │ App 3    │
   │ (Node.js)│      │ (Node.js)│     │ (Node.js)│
   └────┬────┘      └────┬────┘     └────┬────┘
        │                │                │
        └────────────────┼────────────────┘
                         │
                    ┌────▼──────┐
                    │ MongoDB    │  (Atlas - cluster UNIQUE)
                    │ + Redis    │  (ElastiCache - instance UNIQUE)
                    └───────────┘
```

> ⚠️ **Question à se poser** : Que se passe-t-il si MongoDB Atlas est indisponible ?

## Stack technique

| Composant | Technologie | Version | Notes |
|-----------|-------------|---------|-------|
| **Frontend** | React | 17.0.2 | SPA hébergée sur S3 |
| **Backend** | Node.js + Express | 14.x | 3 instances EC2 |
| **Base de données** | MongoDB Atlas | 4.4 | Cluster mutualisé M10 (UNIQUE) |
| **Cache** | Redis | 6.x | ElastiCache (instance UNIQUE) |
| **Stockage fichiers** | AWS S3 | - | Bucket unique |
| **Authentification** | JWT | HS256 | Tokens signés |
| **CI/CD** | GitHub Actions | - | Déploiement auto sur push main |

---

# EXTRAITS DE CODE SOURCE

## Extrait 1 : Authentification (auth.controller.js)

```javascript
// controllers/auth.controller.js
const jwt = require('jsonwebtoken');
const User = require('../models/User');

const JWT_SECRET = 'devsecure2024!';  // ❌ Clé en dur dans le code

exports.login = async (req, res) => {
    const { email, password } = req.body;
    
    try {
        // Recherche utilisateur
        const user = await User.findOne({ email: email });
        
        if (!user) {
            return res.status(401).json({ error: 'Email ou mot de passe incorrect' });
        }
        
        // ❌ Vérification mot de passe en clair (pas de hash)
        if (user.password !== password) {
            return res.status(401).json({ error: 'Email ou mot de passe incorrect' });
        }
        
        // Génération du token JWT
        const token = jwt.sign(
            { userId: user._id, email: user.email, role: user.role },
            JWT_SECRET,
            { expiresIn: '30d' }  // ❌ Très long (30 jours)
        );
        
        res.json({ token, user: { email: user.email, name: user.name } });
        
    } catch (error) {
        // ❌ Logs sensibles (email et password)
        console.log('Erreur login:', email, password, error);
        res.status(500).json({ error: 'Erreur serveur' });
    }
};
```

**Vulnérabilités identifiées :**
- ❌ Secret JWT en dur dans le code (A02)
- ❌ Mot de passe non hashé (A02)
- ❌ Comparaison directe (pas de bcrypt)
- ❌ Tokens très long (30 jours)
- ❌ Logs contenant email/password (A09)

---

## Extrait 2 : Récupération de projet (project.controller.js)

```javascript
// controllers/project.controller.js
const Project = require('../models/Project');

exports.getProject = async (req, res) => {
    const projectId = req.params.id;
    
    try {
        // ❌ Construction de requête non sécurisée
        const query = `{ "_id": "${projectId}" }`;
        const project = await Project.findOne(JSON.parse(query));
        
        if (!project) {
            return res.status(404).json({ error: 'Projet non trouvé' });
        }
        
        // ❌ Pas de vérification d'accès (IDOR possible)
        res.json(project);
        
    } catch (error) {
        res.status(500).json({ error: error.message });
    }
};

exports.searchProjects = async (req, res) => {
    const searchTerm = req.query.q;
    
    // ❌ NoSQL injection : $where avec variables non sécurisées
    const projects = await Project.find({
        $where: `this.title.includes('${searchTerm}') || this.description.includes('${searchTerm}')`
    });
    
    // ❌ Pas de pagination
    res.json(projects);
};
```

**Vulnérabilités identifiées :**
- ❌ Construction JSON dangeureuse (A03 - Injection)
- ❌ Pas de validation d'entrée
- ❌ IDOR possible (A01 - Broken Access Control)
- ❌ NoSQL injection via $where (A03)
- ❌ Pas de limite de résultats (DoS)

---

## Extrait 3 : Upload de fichiers (upload.controller.js)

```javascript
// controllers/upload.controller.js
const AWS = require('aws-sdk');
const path = require('path');

// ❌ Clés AWS en dur dans le code
const s3 = new AWS.S3({
    accessKeyId: 'AKIAIOSFODNN7EXAMPLE',
    secretAccessKey: 'wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY',
    region: 'eu-west-1'
});

exports.uploadFile = async (req, res) => {
    const file = req.files.document;
    const projectId = req.body.projectId;
    
    // ❌ Nom de fichier non validé (path traversal possible)
    const fileName = file.name;  // ../../etc/passwd ?
    const s3Key = `projects/${projectId}/${fileName}`;
    
    const params = {
        Bucket: 'devsecure-files',
        Key: s3Key,
        Body: file.data,
        ACL: 'public-read'  // ❌ Fichiers publiquement accessibles
    };
    
    try {
        await s3.upload(params).promise();
        
        const fileUrl = `https://devsecure-files.s3.eu-west-1.amazonaws.com/${s3Key}`;
        
        res.json({ url: fileUrl, message: 'Fichier uploadé avec succès' });
        
    } catch (error) {
        res.status(500).json({ error: 'Erreur upload' });
    }
};
```

**Vulnérabilités identifiées :**
- ❌ Clés AWS en dur (A02)
- ❌ Pas de validation de nom de fichier (A01 - Path Traversal)
- ❌ ACL public-read = fichiers accessibles publiquement (A01)
- ❌ Pas de limite de taille
- ❌ Pas de type MIME validé

---

## Extrait 4 : Affichage des commentaires (frontend - Comments.jsx)

```jsx
// components/Comments.jsx
import React from 'react';

function Comments({ comments }) {
    return (
        <div className="comments-section">
            <h3>Commentaires ({comments.length})</h3>
            {comments.map((comment, index) => (
                <div key={index} className="comment">
                    <strong>{comment.author}</strong>
                    {/* ❌ XSS : contenu non échappé */}
                    <p dangerouslySetInnerHTML={{ __html: comment.content }} />
                    <small>{comment.date}</small>
                </div>
            ))}
        </div>
    );
}

export default Comments;
```

**Vulnérabilités identifiées :**
- ❌ XSS (Cross-Site Scripting) via `dangerouslySetInnerHTML` (A03)
- ❌ Pas de sanitization de `comment.content`
- ❌ Si quelqu'un rentre `<img src=x onerror="steal()">` → exécuté

---

## Extrait 5 : Configuration API (app.js)

```javascript
// app.js
const express = require('express');
const cors = require('cors');
const app = express();

// ❌ CORS trop permissif
app.use(cors());  // Accepte TOUTES les origines

// ❌ Limite JSON énorme
app.use(express.json({ limit: '50mb' }));  // Risque DoS

// Routes
app.use('/api/auth', require('./routes/auth'));
app.use('/api/projects', require('./routes/projects'));
app.use('/api/users', require('./routes/users'));
app.use('/api/upload', require('./routes/upload'));

// Gestion d'erreurs
app.use((err, req, res, next) => {
    console.error(err.stack);
    // ❌ Stack trace en réponse = info disclosure
    res.status(500).json({ 
        error: err.message,
        stack: err.stack  // Révèle structure du code
    });
});

module.exports = app;
```

**Vulnérabilités identifiées :**
- ❌ CORS sans restriction (A05 - Misconfiguration)
- ❌ Limite JSON énorme = DoS possible
- ❌ Stack trace dans réponse erreur (A09 - Logging failures)
- ❌ Pas de rate limiting
- ❌ Pas d'authentification middleware global

---

# GESTION DES DONNÉES

## Base de données

La base MongoDB Atlas est hébergée sur un **cluster mutualisé unique** (plan M10). Les collections principales :

- `users` : informations utilisateurs (email, mot de passe, rôle)
- `projects` : projets des clients
- `tasks` : tâches liées aux projets
- `comments` : commentaires sur les tâches
- `files` : métadonnées des fichiers uploadés

**⚠️ CRITIQUE : Les mots de passe sont stockés EN CLAIR** dans la collection users "pour faciliter le support en cas d'oubli".

> ⚠️ **Question à se poser** : Que se passe-t-il si cette base est compromise ? 2 000 utilisateurs avec mots de passe en clair = INCIDENT ÉNORME.

## Sauvegardes et continuité

| Élément | Situation actuelle |
|---------|-------------------|
| **Sauvegardes** | Snapshots automatiques MongoDB Atlas (quotidiens) |
| **Tests de restauration** | **Jamais effectués** |
| **Réplication** | Cluster unique, pas de réplication cross-région |
| **Plan de reprise** | **Inexistant** – "On verra si ça arrive" |
| **RTO défini** | Non défini – clients attendent 24/7 |
| **RPO défini** | Non défini – sauvegardes quotidiennes = jusqu'à 24h de perte |

---

# ORGANISATION ET PROCÉDURES

## Équipe de développement

L'équipe de 8 développeurs travaille en mode agile avec des sprints de 2 semaines. Le lead dev (**Thomas, 28 ans**) est présent depuis la création et détient l'essentiel des connaissances techniques.

**Pratiques de développement :**

| Pratique | État |
|----------|------|
| Revue de code | **Non systématique** – "on fait confiance" |
| Tests automatisés | Tests unitaires partiels, **pas de tests de sécurité** |
| Environnement de staging | **Inexistant** – "on teste en prod si besoin" |
| Documentation technique | **Dans la tête de Thomas** |
| Déploiement | Automatique sur push vers `main` |

> ⚠️ **SPOF HUMAIN** : Que se passe-t-il si Thomas est absent 1 mois ?

---

## Gestion des accès

| Élément | Situation |
|---------|-----------|
| Accès AWS | **Tous les développeurs ont un accès administrateur** |
| Clés API AWS | Partagées dans un fichier `.env` **sur Slack** |
| Mot de passe MongoDB | Identique pour tous : `DevSecure2024!` |
| Tokens JWT | Expirent après **30 jours** |
| Comptes anciens employés | Parfois actifs plusieurs semaines après départ |

> ⚠️ **TRÈS DANGEREUX** : Clés AWS sur Slack = n'importe qui peut les récupérer

---

## Politique de sécurité

| Élément | État |
|---------|------|
| Charte informatique | **Inexistante** |
| Formation cybersécurité | **Jamais dispensée** |
| Audit de sécurité | **Jamais réalisé** – "trop cher" |
| Programme bug bounty | Non |

---

# DÉPENDANCES ET SUPPLY CHAIN

## Packages npm

Le fichier `package.json` contient **147 dépendances** directes. Dernière mise à jour : **8 mois**.

```json
{
  "dependencies": {
    "express": "4.17.1",
    "jsonwebtoken": "8.5.1",
    "mongoose": "5.12.3",
    "lodash": "4.17.20",
    "moment": "2.29.1"
  }
}
```

| Pratique | État |
|----------|------|
| `npm audit` | **Jamais exécuté** |
| Dependabot | Non configuré |
| SBOM (Software Bill of Materials) | Inexistant |
| Scanning en CI/CD | Non |

> ⚠️ **Question à se poser** : Combien de CVE dans ces 147 packages vieux de 8 mois ? (Probablement 50+ dont plusieurs CRITIQUES)

---

## Services tiers (supply chain)

| Service | Usage | Criticité | Accès |
|---------|-------|-----------|-------|
| GitHub | Code source | **CRITIQUE** | Tous les devs (admin) |
| AWS | Infrastructure | **CRITIQUE** | Clés partagées |
| MongoDB Atlas | Base de données | **CRITIQUE** | Mot de passe commun |
| Slack | Communication | ÉLEVÉE | Fichiers sensibles partagés |
| Stripe | Paiements | ÉLEVÉE | Clés en variables d'env |

---

# INCIDENTS RÉCENTS

| Date | Incident | Résolution | Durée | Leçons tirées |
|------|----------|------------|-------|---------------|
| **Février 2024** | Fuite de données : fichiers clients accessibles publiquement sur S3 | Modification ACL bucket | Exposition **3 semaines** | Aucune |
| **Mai 2024** | Indisponibilité : erreur de déploiement en prod | Rollback manuel par Thomas | **2h d'arrêt** | "Il faudrait un staging" |
| **Septembre 2024** | Plainte client : accès aux projets d'autres clients (IDOR) | "Correction du bug" | Inconnu | Thomas a dit que c'était corrigé |
| **Novembre 2024** | Alerte : tentatives de connexion suspectes sur l'API | **AUCUNE ACTION** | En cours | "On surveillera" |

---

# CONFORMITÉ ET RÉSILIENCE

## Situation réglementaire

| Réglementation | Situation DevSecure |
|----------------|---------------------|
| **RGPD** | Politique de confidentialité rédigée, **pas de DPO** |
| **NIS2** | Non évalué – "ça ne nous concerne pas" |
| **DORA** | Non concerné (pas secteur financier) |
| **Notification incidents** | Pas de procédure définie |

> ⚠️ Avec des données de 2 000 utilisateurs, DevSecure est soumis au RGPD et doit notifier la CNIL en cas de violation en 72h.

---

## Indicateurs de résilience (non définis)

| Indicateur | Valeur actuelle | Commentaire |
|------------|-----------------|-------------|
| **RTO** (Recovery Time Objective) | **Non défini** | Clients attendent 24/7 |
| **RPO** (Recovery Point Objective) | **~24h** (implicite) | Sauvegardes quotidiennes |
| **MTTR** (Mean Time To Recover) | **Inconnu** | Jamais mesuré |
| **Tests de continuité** | **Jamais réalisés** | "On verra si ça arrive" |

---

## Les 4 piliers de la résilience – État DevSecure

| Pilier | État | Commentaire |
|--------|------|-------------|
| **Anticiper** | ❌ | Pas d'analyse de risques, pas de tests de sécurité |
| **Résister** | ⚠️ | WAF basique CloudFlare, mais pas de rate limiting |
| **Absorber** | ❌ | Pas de mode dégradé, pas de feature flags |
| **Se rétablir** | ❌ | Pas de PRA, sauvegardes non testées |

---

# PROJETS EN COURS

Le CEO indique les priorités pour 2025-2026 :

1. **Lever une série A** (priorité absolue)
2. **Peut-être un audit de sécurité**, si le budget le permet
3. **Recruter un DevOps** pour soulager Thomas
4. **Mettre en place un environnement de staging**

---

# AIDE À L'ANALYSE

## Rappel des 5 composants de Laudon

| Composant | Ce qu'il faut examiner chez DevSecure |
|-----------|---------------------------------------|
| **M** - Matériel | Infrastructure AWS, MongoDB Atlas, Redis |
| **L** - Logiciel | Code applicatif, dépendances npm (147 packages), frameworks |
| **D** - Données | Base MongoDB (mots de passe en clair !), fichiers S3 (publics), sauvegardes non testées |
| **P** - Procédures | CI/CD automatique, pas de revue de code, pas de tests de sécurité |
| **H** - Personnel | Thomas (SPOF), pas de formation, accès trop permissifs |

---

## SPOF à rechercher

| Type | Exemple dans DevSecure | Risque |
|------|------------------------|--------|
| 🖥️ **SPOF Matériel** | Cluster MongoDB UNIQUE | Si down = tout s'arrête |
| 💾 **SPOF Logiciel** | 147 dépendances npm (8 mois outdated) | Log4Shell-like = 0 jour |
| 📊 **SPOF Données** | Sauvegarde unique MongoDB, pas testée | RPO = 24h de perte |
| 👤 **SPOF Humain** | Thomas détient toute la connaissance | Absent = bloqué |
| 📋 **SPOF Procédure** | Pas de staging, déploiement auto | Erreur = production cassée |

---

## Matrice EBIOS pour l'évaluation

| V × I | 🟢 FAIBLE | 🟡 MODÉRÉ | 🟠 ÉLEVÉ | 🔴 CRITIQUE |
|-------|-----------|-----------|----------|-------------|
| Score | 1-3 | 4-7 | 8-11 | 12-16 |
| Action | Surveillance | 3-6 mois | 1 mois | IMMÉDIATE |

**Exemples attendus :**
- Mots de passe en clair = 4 × 4 = 16 = CRITIQUE
- MongoDB SPOF = 4 × 4 = 16 = CRITIQUE
- npm outdated = 4 × 3 = 12 = CRITIQUE
- Thomas absent = 3 × 4 = 12 = CRITIQUE
- XSS dans commentaires = 3 × 2 = 6 = MODÉRÉ

---

*Document transmis par DevSecure – Janvier 2025*
*À usage exclusif de l'auditeur sécurité*

*Bonne chance ! DevSecure a BEAUCOUP de vulnérabilités à trouver...*
