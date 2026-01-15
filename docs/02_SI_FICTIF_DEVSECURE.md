# DESCRIPTION DU SYSTÃˆME D'INFORMATION
## Startup DevSecure â€” Plateforme SaaS de gestion de projets

**Document Ã©tudiant SLAM â€” SÃ©ance 1**

---

> **Contexte** : Vous Ãªtes dÃ©veloppeur sÃ©curitÃ© (DevSecOps) en mission d'audit. La startup DevSecure vous a transmis cette description de leur SI et des extraits de code. 
>
> **Votre mission** : 
> 1. Identifier TOUTES les vulnÃ©rabilitÃ©s (infrastructure ET code)
> 2. Les classer par **composant Laudon** (M, L, D, P, H) et **catÃ©gorie OWASP**
> 3. Identifier les **SPOF** (points uniques de dÃ©faillance)
> 4. Ã‰valuer les risques avec la **mÃ©thode EBIOS** (V Ã— I)

---

# PRÃ‰SENTATION DE L'ENTREPRISE

DevSecure est une startup fondÃ©e en 2021, spÃ©cialisÃ©e dans le dÃ©veloppement d'une plateforme SaaS de gestion de projets collaboratifs destinÃ©e aux PME. L'Ã©quipe est composÃ©e de 12 personnes, principalement des dÃ©veloppeurs.

| DonnÃ©e | Valeur |
|--------|--------|
| **Effectif** | 12 personnes (8 dÃ©veloppeurs, 2 commerciaux, 1 CEO, 1 office manager) |
| **Chiffre d'affaires** | 450 Kâ‚¬ (2024) |
| **Clients** | 85 PME (environ 2 000 utilisateurs actifs) |
| **DonnÃ©es hÃ©bergÃ©es** | Projets, tÃ¢ches, fichiers, donnÃ©es clients |
| **Locaux** | Espace coworking Ã  Lyon Part-Dieu |
| **Contraintes mÃ©tier** | DisponibilitÃ© 24/7 attendue par les clients |

---

# ARCHITECTURE TECHNIQUE

## Infrastructure

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                        INTERNET                              â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                          â”‚
                    â”Œâ”€â”€â”€â”€â”€â–¼â”€â”€â”€â”€â”€â”
                    â”‚  CloudFlare â”‚  (CDN + WAF basique)
                    â””â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”˜
                          â”‚
              â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â–¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
              â”‚   Load Balancer AWS   â”‚
              â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                          â”‚
         â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
         â”‚                â”‚                â”‚
    â”Œâ”€â”€â”€â”€â–¼â”€â”€â”€â”€â”     â”Œâ”€â”€â”€â”€â–¼â”€â”€â”€â”€â”     â”Œâ”€â”€â”€â”€â–¼â”€â”€â”€â”€â”
    â”‚ App 1   â”‚     â”‚ App 2   â”‚     â”‚ App 3   â”‚
    â”‚ (Node)  â”‚     â”‚ (Node)  â”‚     â”‚ (Node)  â”‚
    â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜     â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜     â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”˜
         â”‚                â”‚                â”‚
         â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
                          â”‚
                    â”Œâ”€â”€â”€â”€â”€â–¼â”€â”€â”€â”€â”€â”
                    â”‚  MongoDB   â”‚  (Atlas - cluster UNIQUE)
                    â”‚  + Redis   â”‚  (ElastiCache - instance UNIQUE)
                    â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

> âš ï¸ **Question Ã  se poser** : Que se passe-t-il si MongoDB Atlas est indisponible ?

## Stack technique

| Composant | Technologie | Version | Notes |
|-----------|-------------|---------|-------|
| **Frontend** | React | 17.0.2 | SPA hÃ©bergÃ©e sur S3 |
| **Backend** | Node.js + Express | Node 14.x | 3 instances EC2 |
| **Base de donnÃ©es** | MongoDB Atlas | 4.4 | Cluster mutualisÃ© M10 (UNIQUE) |
| **Cache** | Redis | 6.x | ElastiCache (instance UNIQUE) |
| **Stockage fichiers** | AWS S3 | - | Bucket unique |
| **Authentification** | JWT | - | Tokens signÃ©s HS256 |
| **CI/CD** | GitHub Actions | - | DÃ©ploiement auto sur push main |

---

# EXTRAITS DE CODE SOURCE

## Extrait 1 : Authentification (auth.controller.js)

```javascript
// controllers/auth.controller.js
const jwt = require('jsonwebtoken');
const User = require('../models/User');

const JWT_SECRET = 'devsecure2024!';  // ClÃ© de signature JWT

exports.login = async (req, res) => {
    const { email, password } = req.body;
    
    try {
        // Recherche utilisateur
        const user = await User.findOne({ email: email });
        
        if (!user) {
            return res.status(401).json({ error: 'Email ou mot de passe incorrect' });
        }
        
        // VÃ©rification mot de passe (comparaison directe)
        if (user.password !== password) {
            return res.status(401).json({ error: 'Email ou mot de passe incorrect' });
        }
        
        // GÃ©nÃ©ration du token JWT
        const token = jwt.sign(
            { userId: user._id, email: user.email, role: user.role },
            JWT_SECRET,
            { expiresIn: '30d' }
        );
        
        res.json({ token, user: { email: user.email, name: user.name } });
        
    } catch (error) {
        console.log('Erreur login:', email, password, error);
        res.status(500).json({ error: 'Erreur serveur' });
    }
};
```

## Extrait 2 : RÃ©cupÃ©ration de projet (project.controller.js)

```javascript
// controllers/project.controller.js
const Project = require('../models/Project');

exports.getProject = async (req, res) => {
    const projectId = req.params.id;
    
    try {
        // RequÃªte MongoDB
        const query = `{ "_id": "${projectId}" }`;
        const project = await Project.findOne(JSON.parse(query));
        
        if (!project) {
            return res.status(404).json({ error: 'Projet non trouvÃ©' });
        }
        
        res.json(project);
        
    } catch (error) {
        res.status(500).json({ error: error.message });
    }
};

exports.searchProjects = async (req, res) => {
    const searchTerm = req.query.q;
    
    // Recherche dans le titre et la description
    const projects = await Project.find({
        $where: `this.title.includes('${searchTerm}') || this.description.includes('${searchTerm}')`
    });
    
    res.json(projects);
};
```

## Extrait 3 : Upload de fichiers (upload.controller.js)

```javascript
// controllers/upload.controller.js
const AWS = require('aws-sdk');
const path = require('path');

const s3 = new AWS.S3({
    accessKeyId: 'AKIAIOSFODNN7EXAMPLE',
    secretAccessKey: 'wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY',
    region: 'eu-west-1'
});

exports.uploadFile = async (req, res) => {
    const file = req.files.document;
    const projectId = req.body.projectId;
    
    // GÃ©nÃ©ration du nom de fichier
    const fileName = file.name;
    const s3Key = `projects/${projectId}/${fileName}`;
    
    const params = {
        Bucket: 'devsecure-files',
        Key: s3Key,
        Body: file.data,
        ACL: 'public-read'
    };
    
    try {
        await s3.upload(params).promise();
        
        // Sauvegarde URL en base
        const fileUrl = `https://devsecure-files.s3.eu-west-1.amazonaws.com/${s3Key}`;
        
        res.json({ url: fileUrl, message: 'Fichier uploadÃ© avec succÃ¨s' });
        
    } catch (error) {
        res.status(500).json({ error: 'Erreur upload' });
    }
};
```

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
                    <p dangerouslySetInnerHTML={{ __html: comment.content }} />
                    <small>{comment.date}</small>
                </div>
            ))}
        </div>
    );
}

export default Comments;
```

## Extrait 5 : Configuration API (app.js)

```javascript
// app.js
const express = require('express');
const cors = require('cors');
const app = express();

// Configuration CORS
app.use(cors());

// Parsing JSON
app.use(express.json({ limit: '50mb' }));

// Routes
app.use('/api/auth', require('./routes/auth'));
app.use('/api/projects', require('./routes/projects'));
app.use('/api/users', require('./routes/users'));
app.use('/api/upload', require('./routes/upload'));

// Gestion d'erreurs
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).json({ 
        error: err.message,
        stack: err.stack 
    });
});

module.exports = app;
```

---

# GESTION DES DONNÃ‰ES

## Base de donnÃ©es

La base MongoDB Atlas est hÃ©bergÃ©e sur un **cluster mutualisÃ© unique** (plan M10). Les collections principales :

- `users` : informations utilisateurs (email, mot de passe, rÃ´le)
- `projects` : projets des clients
- `tasks` : tÃ¢ches liÃ©es aux projets
- `comments` : commentaires sur les tÃ¢ches
- `files` : mÃ©tadonnÃ©es des fichiers uploadÃ©s

Les mots de passe sont stockÃ©s **en clair** dans la collection users Â« pour faciliter le support en cas d'oubli Â».

> âš ï¸ **Question Ã  se poser** : Que se passe-t-il si cette base est compromise ?

## Sauvegardes et continuitÃ©

| Ã‰lÃ©ment | Situation actuelle |
|---------|-------------------|
| **Sauvegardes** | Snapshots automatiques MongoDB Atlas (quotidiens) |
| **Tests de restauration** | **Jamais effectuÃ©s** |
| **RÃ©plication** | Cluster unique, pas de rÃ©plication cross-rÃ©gion |
| **Plan de reprise** | **Inexistant** â€” Â« On verra si Ã§a arrive Â» |
| **RTO dÃ©fini** | Non dÃ©fini â€” clients attendent 24/7 |
| **RPO dÃ©fini** | Non dÃ©fini â€” sauvegardes quotidiennes = jusqu'Ã  24h de perte |

---

# ORGANISATION ET PROCÃ‰DURES

## Ã‰quipe de dÃ©veloppement

L'Ã©quipe de 8 dÃ©veloppeurs travaille en mode agile avec des sprints de 2 semaines. Le lead dev (**Thomas, 28 ans**) est prÃ©sent depuis la crÃ©ation et dÃ©tient l'essentiel des connaissances techniques.

**Pratiques de dÃ©veloppement :**

| Pratique | Ã‰tat |
|----------|------|
| Revue de code | **Non systÃ©matique** â€” Â« on fait confiance Â» |
| Tests automatisÃ©s | Tests unitaires partiels, pas de tests de sÃ©curitÃ© |
| Environnement de staging | **Inexistant** â€” Â« on teste en prod si besoin Â» |
| Documentation technique | **Dans la tÃªte de Thomas** |
| DÃ©ploiement | Automatique sur push vers `main` |

> âš ï¸ **Question Ã  se poser** : Que se passe-t-il si Thomas est absent 1 mois ?

## Gestion des accÃ¨s

| Ã‰lÃ©ment | Situation |
|---------|-----------|
| AccÃ¨s AWS | **Tous les dÃ©veloppeurs ont un accÃ¨s administrateur** |
| ClÃ©s API AWS | PartagÃ©es dans un fichier `.env` **sur Slack** |
| Mot de passe MongoDB | Identique pour tous : `DevSecure2024!` |
| Tokens JWT | Expirent aprÃ¨s **30 jours** |
| Comptes anciens employÃ©s | Parfois actifs plusieurs semaines aprÃ¨s dÃ©part |

## Politique de sÃ©curitÃ©

| Ã‰lÃ©ment | Ã‰tat |
|---------|------|
| Charte informatique | **Inexistante** |
| Formation cybersÃ©curitÃ© | **Jamais dispensÃ©e** |
| Audit de sÃ©curitÃ© | **Jamais rÃ©alisÃ©** â€” Â« trop cher Â» |
| Programme bug bounty | Non |

---

# DÃ‰PENDANCES ET SUPPLY CHAIN

## Packages npm

Le fichier `package.json` contient **147 dÃ©pendances** directes. DerniÃ¨re mise Ã  jour : **8 mois**.

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

| Pratique | Ã‰tat |
|----------|------|
| `npm audit` | **Jamais exÃ©cutÃ©** |
| Dependabot | Non configurÃ© |
| SBOM (Software Bill of Materials) | Inexistant |

> âš ï¸ **Question Ã  se poser** : Combien de CVE dans ces 147 packages vieux de 8 mois ?

## Services tiers (supply chain)

| Service | Usage | Niveau de dÃ©pendance | AccÃ¨s |
|---------|-------|---------------------|-------|
| GitHub | Code source | **CRITIQUE** | Tous les devs (admin) |
| AWS | Infrastructure | **CRITIQUE** | ClÃ©s partagÃ©es |
| MongoDB Atlas | Base de donnÃ©es | **CRITIQUE** | Mot de passe commun |
| Slack | Communication | Ã‰LEVÃ‰ | Fichiers sensibles partagÃ©s |
| Stripe | Paiements | Ã‰LEVÃ‰ | ClÃ©s en variables d'env |

---

# INCIDENTS RÃ‰CENTS

| Date | Incident | RÃ©solution | DurÃ©e | LeÃ§ons tirÃ©es |
|------|----------|------------|-------|---------------|
| **FÃ©vrier 2024** | Fuite de donnÃ©es : fichiers clients accessibles publiquement sur S3 | Modification ACL bucket | Exposition **3 semaines** | Aucune |
| **Mai 2024** | IndisponibilitÃ© : erreur de dÃ©ploiement en prod | Rollback manuel par Thomas | **2h d'arrÃªt** | Â« Il faudrait un staging Â» |
| **Septembre 2024** | Plainte client : accÃ¨s aux projets d'autres clients (IDOR) | Â« Correction du bug Â» | Inconnu | Thomas a dit que c'Ã©tait corrigÃ© |
| **Novembre 2024** | Alerte : tentatives de connexion suspectes sur l'API | **Aucune action** | En cours | Â« On surveillera Â» |

---

# CONFORMITÃ‰ ET RÃ‰SILIENCE

## Situation rÃ©glementaire

| RÃ©glementation | Situation DevSecure |
|----------------|---------------------|
| **RGPD** | Politique de confidentialitÃ© rÃ©digÃ©e, **pas de DPO** |
| **NIS2** | Non Ã©valuÃ© â€” Â« Ã§a ne nous concerne pas Â» |
| **DORA** | Non concernÃ© (pas secteur financier) |
| **Notification incidents** | Pas de procÃ©dure dÃ©finie |

## Indicateurs de rÃ©silience (non dÃ©finis)

| Indicateur | Valeur actuelle | Commentaire |
|------------|-----------------|-------------|
| **RTO** (Recovery Time Objective) | **Non dÃ©fini** | Clients attendent 24/7 |
| **RPO** (Recovery Point Objective) | **~24h** (implicite) | Sauvegardes quotidiennes |
| **MTTR** (Mean Time To Recover) | **Inconnu** | Jamais mesurÃ© |
| **Tests de continuitÃ©** | **Jamais rÃ©alisÃ©s** | Â« On verra si Ã§a arrive Â» |

## Les 4 piliers de la rÃ©silience â€” Ã‰tat DevSecure

| Pilier | Ã‰tat | Commentaire |
|--------|------|-------------|
| **Anticiper** | âŒ | Pas d'analyse de risques, pas de tests de sÃ©curitÃ© |
| **RÃ©sister** | âš ï¸ | WAF basique CloudFlare, mais pas de rate limiting |
| **Absorber** | âŒ | Pas de mode dÃ©gradÃ©, pas de feature flags |
| **Se rÃ©tablir** | âŒ | Pas de PRA, sauvegardes non testÃ©es |

---

# PROJETS EN COURS

Le CEO indique les prioritÃ©s pour 2025-2026 :

1. Â« Lever une sÃ©rie A Â» (prioritÃ© absolue)
2. Â« Peut-Ãªtre un audit de sÃ©curitÃ©, si le budget le permet Â»
3. Â« Recruter un DevOps pour soulager Thomas Â»
4. Â« Mettre en place un environnement de staging Â»

---

*Document transmis par DevSecure â€” Janvier 2025*
*Ã€ usage exclusif de l'auditeur sÃ©curitÃ©*

---

# AIDE Ã€ L'ANALYSE

## Rappel des 5 composants de Laudon

| Composant | Ce qu'il faut examiner chez DevSecure |
|-----------|---------------------------------------|
| **M** - MatÃ©riel | Infrastructure AWS, MongoDB Atlas, Redis |
| **L** - Logiciel | Code applicatif, dÃ©pendances npm, frameworks |
| **D** - DonnÃ©es | Base MongoDB, fichiers S3, sauvegardes, logs |
| **P** - ProcÃ©dures | CI/CD, revue de code, documentation, PRA |
| **H** - Personnel | Thomas (lead dev), formation, compÃ©tences |

## Types de SPOF Ã  rechercher

- ðŸ–¥ï¸ **SPOF MatÃ©riel** : Serveur/service unique sans redondance
- ðŸ’¿ **SPOF Logiciel** : DÃ©pendance critique unique
- ðŸ“Š **SPOF DonnÃ©es** : Sauvegarde unique ou non testÃ©e
- ðŸ‘¤ **SPOF Humain** : Personne unique dÃ©tenant un savoir critique
- ðŸ“‹ **SPOF ProcÃ©dure** : Processus unique sans alternative

## Matrice EBIOS pour l'Ã©valuation

| V Ã— I | ðŸŸ¢ FAIBLE | ðŸŸ¡ MODÃ‰RÃ‰ | ðŸŸ  Ã‰LEVÃ‰ | ðŸ”´ CRITIQUE |
|-------|-----------|-----------|----------|-------------|
| Score | 1-3 | 4-7 | 8-11 | 12-16 |
| Action | Surveillance | 3-6 mois | 1 mois | ImmÃ©diate |
