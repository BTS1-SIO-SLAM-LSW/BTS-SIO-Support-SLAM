# SUPPORT DE COURS
## SÃ©ance 1 â€” Cartographier la vulnÃ©rabilitÃ©
### Analyse de risques et cybersÃ©curitÃ© du SI

**BTS SIO â€” Bloc 3 â€” CompÃ©tence C1 : Analyser un risque informatique**

---

## ðŸ“‹ SOMMAIRE

1. [Ã‰tude de cas : L'incident CrowdStrike (19 juillet 2024)](#1-Ã©tude-de-cas--lincident-crowdstrike)
2. [Les 5 composants du SystÃ¨me d'Information (Laudon)](#2-les-5-composants-du-systÃ¨me-dinformation)
3. [VulnÃ©rabilitÃ©, Menace, Risque : les fondamentaux](#3-vulnÃ©rabilitÃ©-menace-risque--les-fondamentaux)
4. [La mÃ©thode EBIOS simplifiÃ©e](#4-la-mÃ©thode-ebios-simplifiÃ©e)
5. [Le concept de SPOF (Single Point of Failure)](#5-le-concept-de-spof)
6. [Introduction Ã  la cyber-rÃ©silience](#6-introduction-Ã -la-cyber-rÃ©silience)
7. [Exercices d'application](#7-exercices-dapplication)

---

# 1. Ã‰TUDE DE CAS : L'incident CrowdStrike

## 1.1 Contexte de l'incident

Le **19 juillet 2024**, une panne informatique mondiale a paralysÃ© des milliers d'organisations pendant plusieurs heures. L'origine : une simple mise Ã  jour logicielle dÃ©fectueuse.

> ðŸ“˜ **CrowdStrike Falcon**
> 
> Logiciel de cybersÃ©curitÃ© de type EDR (Endpoint Detection and Response) installÃ© sur des millions d'ordinateurs Windows dans le monde. Il surveille et protÃ¨ge les systÃ¨mes contre les menaces.

## 1.2 Chronologie des Ã©vÃ©nements

| Heure (UTC) | Ã‰vÃ©nement |
|-------------|-----------|
| 04:09 | CrowdStrike dÃ©ploie la mise Ã  jour du fichier de canal 291 |
| 04:09 - 05:27 | Les machines Windows redÃ©marrent avec un Ã©cran bleu (BSOD) |
| 05:27 | CrowdStrike identifie le problÃ¨me et stoppe le dÃ©ploiement |
| 06:00 - 12:00 | Chaos mondial : aÃ©roports, banques, hÃ´pitaux paralysÃ©s |
| 12:00+ | DÃ©but des opÃ©rations de rÃ©cupÃ©ration manuelle |

## 1.3 Impact mondial

| Indicateur | Valeur | Commentaire |
|------------|--------|-------------|
| Machines touchÃ©es | **8,5 millions** | Environ 1% du parc Windows mondial |
| Vols annulÃ©s | **Plus de 3 000** | Delta, United, Air France... |
| Pertes Ã©conomiques | **5,4 milliards $** | Estimation Fortune 500 uniquement |
| DurÃ©e de perturbation | **24 Ã  72 heures** | Selon les organisations |

> ðŸ’¡ **Organisations touchÃ©es**
> 
> Delta Air Lines (1 300 vols annulÃ©s, 500 M$ de pertes), NHS (hÃ´pitaux britanniques), Sky News (Ã©cran noir en direct), banques (distributeurs hors service), supermarchÃ©s (caisses bloquÃ©es).

## 1.4 Analyse de la cause

La mise Ã  jour contenait une **erreur de programmation** qui provoquait un crash du pilote (driver) Windows au dÃ©marrage. Le problÃ¨me : cette mise Ã  jour s'est dÃ©ployÃ©e **automatiquement**, sans validation prÃ©alable par les clients.

> ðŸ”‘ **Ã€ RETENIR**
> 
> Une organisation peut Ãªtre parfaitement sÃ©curisÃ©e en interne et pourtant Ãªtre paralysÃ©e par la dÃ©faillance d'un fournisseur. C'est le risque Â« supply chain Â».

## 1.5 LeÃ§ons Ã  retenir

- L'interdÃ©pendance des systÃ¨mes crÃ©e des **effets domino** imprÃ©visibles
- Un fournisseur critique (comme un antivirus) peut devenir un **point de dÃ©faillance**
- La confiance aveugle dans les mises Ã  jour automatiques est risquÃ©e
- La prÃ©paration Ã  la crise (plans de continuitÃ©) est **essentielle**

---

# 2. LES 5 COMPOSANTS DU SYSTÃˆME D'INFORMATION

## 2.1 Le modÃ¨le de Laudon & Laudon

Kenneth et Jane Laudon, auteurs de rÃ©fÃ©rence en systÃ¨mes d'information, proposent une vision systÃ©mique du SI articulÃ©e autour de **5 composants interdÃ©pendants**.

> ðŸ“˜ **SystÃ¨me d'Information (SI)**
> 
> Ensemble organisÃ© de ressources (matÃ©riel, logiciel, donnÃ©es, procÃ©dures, personnel) permettant de collecter, stocker, traiter et diffuser l'information au sein d'une organisation.

## 2.2 Les 5 composants dÃ©taillÃ©s

| Composant | Description | Exemples concrets |
|-----------|-------------|-------------------|
| **M - MatÃ©riel** (Hardware) | Infrastructure physique du SI | Serveurs, postes de travail, routeurs, switches, cÃ¢blage, onduleurs |
| **L - Logiciel** (Software) | Programmes et applications | SystÃ¨mes d'exploitation, ERP, antivirus, applications mÃ©tier |
| **D - DonnÃ©es** (Data) | Informations stockÃ©es et traitÃ©es | Bases de donnÃ©es, fichiers, sauvegardes, logs |
| **P - ProcÃ©dures** (Procedures) | RÃ¨gles et processus d'utilisation | Politiques de sÃ©curitÃ©, documentation, workflows, PCA/PRA |
| **H - Personnel** (People) | Ressources humaines du SI | Utilisateurs, administrateurs, DSI, RSSI, DPO |

> ðŸ”‘ **MnÃ©monique**
> 
> **MLDPP** = Â« **M**a **L**igne **D**e **P**rotection **P**ermanente Â»
> 
> ou simplement : MatÃ©riel - Logiciel - DonnÃ©es - ProcÃ©dures - Personnel

## 2.3 L'interdÃ©pendance des composants

Le point crucial du modÃ¨le de Laudon est l'**interdÃ©pendance** : chaque composant dÃ©pend des autres pour fonctionner correctement.

```
        ðŸ–¥ï¸ MATÃ‰RIEL
             â†•ï¸
        ðŸ’¿ LOGICIEL
             â†•ï¸
        ðŸ“Š DONNÃ‰ES
             â†•ï¸
   ðŸ“‹ PROCÃ‰DURES  â†â†’  ðŸ‘¥ PERSONNEL

   Tous interconnectÃ©s : une dÃ©faillance 
   sur l'un impacte les autres
```

> ðŸ’¡ **Exemple d'interdÃ©pendance (CrowdStrike)**
> 
> Le composant LOGICIEL (mise Ã  jour CrowdStrike) a rendu le MATÃ‰RIEL inutilisable (Ã©cran bleu), les DONNÃ‰ES inaccessibles, les PROCÃ‰DURES impossibles Ã  exÃ©cuter, et le PERSONNEL incapable de travailler.

## 2.4 Application Ã  l'analyse de risques

Pour analyser la sÃ©curitÃ© d'un SI, il faut examiner **CHAQUE composant** sÃ©parÃ©ment, puis leurs interactions :

- Le matÃ©riel est-il rÃ©cent et maintenu ?
- Les logiciels sont-ils Ã  jour et sÃ©curisÃ©s ?
- Les donnÃ©es sont-elles sauvegardÃ©es et protÃ©gÃ©es ?
- Les procÃ©dures sont-elles documentÃ©es et appliquÃ©es ?
- Le personnel est-il formÃ© et sensibilisÃ© ?

---

# 3. VULNÃ‰RABILITÃ‰, MENACE, RISQUE : LES FONDAMENTAUX

## 3.1 DÃ©finitions essentielles

> ðŸ“˜ **VulnÃ©rabilitÃ©**
> 
> **Faiblesse** d'un systÃ¨me qui pourrait Ãªtre exploitÃ©e. C'est une caractÃ©ristique **intrinsÃ¨que** du systÃ¨me.
> 
> *Exemple : un serveur non mis Ã  jour, un mot de passe faible, l'absence de sauvegarde.*

> ðŸ“˜ **Menace**
> 
> Ã‰vÃ©nement potentiel qui pourrait **exploiter une vulnÃ©rabilitÃ©** et causer un dommage. C'est **externe** au systÃ¨me.
> 
> *Exemple : un hacker, un virus, une panne Ã©lectrique, un incendie, une erreur humaine.*

> ðŸ“˜ **Risque**
> 
> Combinaison de la **probabilitÃ©** qu'une menace exploite une vulnÃ©rabilitÃ© et de l'**impact** qui en rÃ©sulterait.
> 
> *Risque = VulnÃ©rabilitÃ© + Menace + Impact potentiel*

## 3.2 La relation entre les concepts

Ces trois concepts sont liÃ©s par une **chaÃ®ne causale** :

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  VULNÃ‰RABILITÃ‰  â†’  exploitÃ©e par  â†’  MENACE  â†’  cause  â†’  IMPACT  =  RISQUE  â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

## 3.3 Exemples concrets

| VulnÃ©rabilitÃ© | Menace | Impact | Risque |
|---------------|--------|--------|--------|
| Serveur non mis Ã  jour | Exploitation d'une faille connue | Prise de contrÃ´le du serveur | **Ã‰LEVÃ‰** |
| Mot de passe faible | Attaque par force brute | AccÃ¨s non autorisÃ© aux donnÃ©es | **Ã‰LEVÃ‰** |
| Sauvegarde sur mÃªme site | Incendie dans les locaux | Perte totale des donnÃ©es | **CRITIQUE** |
| Personnel non formÃ© | Email de phishing | Vol d'identifiants | **Ã‰LEVÃ‰** |
| Antivirus gratuit | Malware rÃ©cent | Infection du parc | **MODÃ‰RÃ‰** |

> âš ï¸ **Attention**
> 
> Une vulnÃ©rabilitÃ© sans menace associÃ©e n'est pas un risque. Un serveur ancien dans une piÃ¨ce fermÃ©e Ã  clÃ© sans connexion rÃ©seau prÃ©sente peu de risques, mÃªme s'il est vulnÃ©rable.

## 3.4 Formule du risque

En analyse de risques, on utilise gÃ©nÃ©ralement la formule :

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚   RISQUE = VRAISEMBLANCE Ã— IMPACT        â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

- **Vraisemblance** : probabilitÃ© que la menace exploite la vulnÃ©rabilitÃ©
- **Impact** : gravitÃ© des consÃ©quences si le risque se rÃ©alise

---

# 4. LA MÃ‰THODE EBIOS SIMPLIFIÃ‰E

## 4.1 PrÃ©sentation d'EBIOS

> ðŸ“˜ **EBIOS Risk Manager**
> 
> MÃ©thode franÃ§aise d'analyse de risques dÃ©veloppÃ©e par l'**ANSSI** (Agence Nationale de la SÃ©curitÃ© des SystÃ¨mes d'Information).
> 
> EBIOS = **E**xpression des **B**esoins et **I**dentification des **O**bjectifs de **S**Ã©curitÃ©

Dans ce cours, nous utilisons une **version simplifiÃ©e** adaptÃ©e au BTS SIO, basÃ©e sur l'Ã©valuation de deux critÃ¨res : la vraisemblance et l'impact.

## 4.2 Ã‰chelle de vraisemblance (V)

| Niveau | LibellÃ© | Description | Exemples |
|--------|---------|-------------|----------|
| **1** | TrÃ¨s improbable | NÃ©cessite des moyens exceptionnels ou des circonstances trÃ¨s rares | Attaque ciblÃ©e par un Ã‰tat-nation, catastrophe naturelle majeure |
| **2** | Peu probable | Possible mais nÃ©cessite des compÃ©tences ou circonstances particuliÃ¨res | Exploitation d'une faille 0-day, intrusion physique sophistiquÃ©e |
| **3** | Probable | Se produit rÃ©guliÃ¨rement dans le secteur d'activitÃ© | Phishing rÃ©ussi, erreur humaine, panne matÃ©rielle courante |
| **4** | TrÃ¨s probable | Quasi certain de se produire Ã  court terme | Exploitation d'une faille connue non corrigÃ©e, Ã©quipement en fin de vie |

## 4.3 Ã‰chelle d'impact (I)

| Niveau | LibellÃ© | Description | Exemples |
|--------|---------|-------------|----------|
| **1** | Mineur | Perturbation limitÃ©e, rÃ©cupÃ©ration rapide, pas de perte significative | IndisponibilitÃ© < 1h, donnÃ©es non sensibles concernÃ©es |
| **2** | Significatif | Perturbation notable mais gÃ©rable, rÃ©cupÃ©ration en quelques heures | IndisponibilitÃ© < 1 jour, donnÃ©es internes exposÃ©es |
| **3** | Grave | ArrÃªt d'activitÃ© partiel, perte de donnÃ©es clients, atteinte Ã  l'image | IndisponibilitÃ© > 1 jour, donnÃ©es personnelles compromises |
| **4** | Critique | ArrÃªt prolongÃ©, menace sur la survie de l'entreprise | Perte donnÃ©es stratÃ©giques, sanctions RGPD, perte de clients majeurs |

## 4.4 Matrice de criticitÃ©

Le niveau de risque est calculÃ© en multipliant la vraisemblance par l'impact :

| V \ I | Impact 1 | Impact 2 | Impact 3 | Impact 4 |
|-------|----------|----------|----------|----------|
| **V = 4** | 4 ðŸŸ¡ | 8 ðŸŸ  | 12 ðŸ”´ | 16 ðŸ”´ |
| **V = 3** | 3 ðŸŸ¢ | 6 ðŸŸ¡ | 9 ðŸŸ  | 12 ðŸ”´ |
| **V = 2** | 2 ðŸŸ¢ | 4 ðŸŸ¡ | 6 ðŸŸ¡ | 8 ðŸŸ  |
| **V = 1** | 1 ðŸŸ¢ | 2 ðŸŸ¢ | 3 ðŸŸ¢ | 4 ðŸŸ¡ |

**LÃ©gende :**
- ðŸ”´ **CRITIQUE** (12-16)
- ðŸŸ  **Ã‰LEVÃ‰** (8-11)
- ðŸŸ¡ **MODÃ‰RÃ‰** (4-7)
- ðŸŸ¢ **FAIBLE** (1-3)

## 4.5 InterprÃ©tation des niveaux de risque

| Niveau | Score | Action requise | DÃ©lai |
|--------|-------|----------------|-------|
| ðŸ”´ **CRITIQUE** | 12-16 | Action immÃ©diate, risque inacceptable | Sous 24-48h |
| ðŸŸ  **Ã‰LEVÃ‰** | 8-11 | Action prioritaire Ã  planifier | Sous 1 mois |
| ðŸŸ¡ **MODÃ‰RÃ‰** | 4-7 | Action Ã  moyen terme | Sous 3-6 mois |
| ðŸŸ¢ **FAIBLE** | 1-3 | Surveillance, action si opportunitÃ© | Lors de la prochaine rÃ©vision |

---

# 5. LE CONCEPT DE SPOF

## 5.1 DÃ©finition

> ðŸ“˜ **SPOF (Single Point of Failure)**
> 
> **Point unique de dÃ©faillance** : composant dont la panne entraÃ®ne l'arrÃªt complet d'un systÃ¨me ou d'un processus. C'est un Ã©lÃ©ment critique **sans redondance** ni plan de secours.

Le terme vient de l'ingÃ©nierie de la fiabilitÃ©. Un SPOF est comme le **maillon faible** d'une chaÃ®ne : si ce maillon cÃ¨de, toute la chaÃ®ne se rompt.

## 5.2 Types de SPOF

| Type de SPOF | Description | Exemples |
|--------------|-------------|----------|
| **SPOF MatÃ©riel** | Ã‰quipement unique sans redondance | Serveur unique, routeur unique, liaison Internet unique |
| **SPOF Logiciel** | Application critique sans alternative | ERP unique, solution de sauvegarde unique |
| **SPOF DonnÃ©es** | DonnÃ©es sans copie de secours | Sauvegarde unique sur mÃªme site |
| **SPOF Humain** | Personne unique dÃ©tenant un savoir critique | Technicien informatique unique, Â« l'expert qui sait tout Â» |
| **SPOF ProcÃ©dure** | Processus sans mode dÃ©gradÃ© | Pas de procÃ©dure de secours documentÃ©e |

## 5.3 Identifier les SPOF

Pour chaque Ã©lÃ©ment critique du SI, posez-vous la question :

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚  Â« Si cet Ã©lÃ©ment tombe en panne, que se passe-t-il ? Â»     â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

Si la rÃ©ponse est **Â« tout s'arrÃªte Â»** ou **Â« on ne peut plus travailler Â»**, vous avez identifiÃ© un SPOF.

## 5.4 Solutions contre les SPOF

| Solution | Description | Exemple |
|----------|-------------|---------|
| **Redondance** | Dupliquer les Ã©lÃ©ments critiques | Deux serveurs en cluster, deux liaisons Internet |
| **Haute disponibilitÃ©** | Basculement automatique en cas de panne | Serveur de secours qui prend le relais |
| **Sauvegarde externalisÃ©e** | Copie des donnÃ©es sur un autre site | Sauvegarde cloud, datacenter de secours |
| **Documentation** | Ã‰viter la dÃ©pendance Ã  une personne | ProcÃ©dures Ã©crites, formation croisÃ©e |
| **Mode dÃ©gradÃ©** | Pouvoir continuer mÃªme partiellement | ProcÃ©dures papier de secours |

> ðŸ’¡ **SPOF dans l'incident CrowdStrike**
> 
> Pour de nombreuses organisations, CrowdStrike Ã©tait un SPOF : un logiciel unique, dÃ©ployÃ© sur tous les postes, sans alternative immÃ©diate. Quand il a dÃ©failli, tout s'est arrÃªtÃ©.

---

# 6. INTRODUCTION Ã€ LA CYBER-RÃ‰SILIENCE

## 6.1 De la sÃ©curitÃ© Ã  la rÃ©silience

Traditionnellement, la cybersÃ©curitÃ© visait Ã  **empÃªcher** les incidents de se produire (prÃ©vention). Mais l'expÃ©rience montre que les incidents sont **inÃ©vitables**. D'oÃ¹ l'Ã©mergence d'un nouveau paradigme : la **cyber-rÃ©silience**.

> ðŸ“˜ **Cyber-rÃ©silience**
> 
> CapacitÃ© d'une organisation Ã  **anticiper, rÃ©sister, absorber et se rÃ©tablir** face Ã  des incidents cyber, tout en maintenant ses fonctions essentielles.
> 
> Ce n'est plus Â« empÃªcher l'incident Â» mais Â« **survivre Ã  l'incident** Â».

## 6.2 Les 4 piliers de la rÃ©silience

| Pilier | Description | Actions concrÃ¨tes |
|--------|-------------|-------------------|
| **1. Anticiper** | Identifier les menaces et vulnÃ©rabilitÃ©s avant qu'elles ne soient exploitÃ©es | Analyse de risques, veille sÃ©curitÃ©, tests de pÃ©nÃ©tration |
| **2. RÃ©sister** | Limiter l'impact d'un incident quand il survient | Segmentation rÃ©seau, dÃ©tection d'intrusion, rÃ©ponse rapide |
| **3. Absorber** | Maintenir les fonctions essentielles malgrÃ© l'incident | Mode dÃ©gradÃ©, PCA (Plan de ContinuitÃ© d'ActivitÃ©) |
| **4. Se rÃ©tablir** | Revenir Ã  un Ã©tat normal le plus rapidement possible | PRA (Plan de Reprise d'ActivitÃ©), sauvegardes testÃ©es |

## 6.3 Indicateurs clÃ©s : RTO et RPO

> ðŸ“˜ **RTO (Recovery Time Objective)**
> 
> **DurÃ©e maximale acceptable** d'interruption d'un service. C'est le temps qu'on se donne pour rÃ©tablir le service aprÃ¨s un incident.
> 
> *Exemple : RTO de 4 heures = le service doit Ãªtre rÃ©tabli en moins de 4 heures.*

> ðŸ“˜ **RPO (Recovery Point Objective)**
> 
> **Perte de donnÃ©es maximale acceptable** en cas d'incident, exprimÃ©e en temps. C'est le Â« retour en arriÃ¨re Â» maximum tolÃ©rable.
> 
> *Exemple : RPO de 1 heure = on accepte de perdre au maximum 1 heure de donnÃ©es.*

> ðŸ’¡ **Application des RTO/RPO**
> 
> Pour un site e-commerce :
> - **RTO = 2h** (on ne peut pas rester hors ligne plus de 2h)
> - **RPO = 15 min** (on ne peut pas perdre plus de 15 min de commandes)
> 
> Cela impose des sauvegardes toutes les 15 min et une infrastructure de secours activable en 2h.

## 6.4 Cadre rÃ©glementaire europÃ©en

La cyber-rÃ©silience est dÃ©sormais une **obligation lÃ©gale** pour de nombreuses organisations :

| RÃ©glementation | Champ d'application | Obligation principale |
|----------------|---------------------|----------------------|
| **NIS2** (2024) | EntitÃ©s essentielles et importantes (18 secteurs) | Analyse de risques, notification 24h, tests de rÃ©silience |
| **DORA** (2025) | Secteur financier (banques, assurances) | Tests de pÃ©nÃ©tration avancÃ©s, gestion des tiers |
| **RGPD** (2018) | Toute organisation traitant des donnÃ©es personnelles | SÃ©curitÃ© des donnÃ©es, notification 72h en cas de violation |

> ðŸ”‘ **Ã€ RETENIR**
> 
> La cyber-rÃ©silience n'est plus optionnelle : c'est une **exigence lÃ©gale** et un **avantage concurrentiel**. Les organisations qui peuvent dÃ©montrer leur rÃ©silience gagnent la confiance de leurs clients et partenaires.

---

# 7. EXERCICES D'APPLICATION

## Exercice 1 : Identifier les composants Laudon

Pour chaque Ã©lÃ©ment ci-dessous, indiquez le composant du SI correspondant (M, L, D, P ou H) :

| Ã‰lÃ©ment | Composant |
|---------|-----------|
| Un serveur Dell PowerEdge | _____ |
| La base de donnÃ©es clients | _____ |
| Le logiciel de comptabilitÃ© Sage | _____ |
| La charte informatique de l'entreprise | _____ |
| Le technicien rÃ©seau | _____ |
| Les sauvegardes quotidiennes | _____ |
| Le systÃ¨me d'exploitation Windows Server | _____ |
| La procÃ©dure de gestion des mots de passe | _____ |

---

## Exercice 2 : Distinguer vulnÃ©rabilitÃ© et menace

Pour chaque situation, identifiez la vulnÃ©rabilitÃ© et la menace :

**a) Un employÃ© reÃ§oit un email de phishing et clique sur le lien malveillant.**

- VulnÃ©rabilitÃ© : ______________________________________
- Menace : ______________________________________

**b) Un hacker exploite une faille connue sur un serveur web non mis Ã  jour.**

- VulnÃ©rabilitÃ© : ______________________________________
- Menace : ______________________________________

**c) Un incendie dÃ©truit la salle serveur oÃ¹ se trouvent les sauvegardes.**

- VulnÃ©rabilitÃ© : ______________________________________
- Menace : ______________________________________

---

## Exercice 3 : Calcul de risque EBIOS

Ã‰valuez le niveau de risque pour chaque situation (V Ã— I) :

| Situation | V (1-4) | I (1-4) | Risque | Niveau |
|-----------|---------|---------|--------|--------|
| Serveur de 10 ans hÃ©bergeant les donnÃ©es clients | | | | |
| Poste de travail avec antivirus Ã  jour | | | | |
| Sauvegarde quotidienne testÃ©e mensuellement | | | | |
| Mot de passe admin partagÃ© entre 5 personnes | | | | |
| WiFi ouvert aux visiteurs sans isolation rÃ©seau | | | | |

---

## Exercice 4 : Identifier les SPOF

Dans la liste suivante, identifiez les SPOF potentiels et proposez une solution :

| Ã‰lÃ©ment | SPOF ? (Oui/Non) | Solution proposÃ©e |
|---------|------------------|-------------------|
| Serveur unique hÃ©bergeant l'ERP | | |
| Deux liaisons Internet (Orange + SFR) | | |
| Technicien informatique unique | | |
| Sauvegardes sur 3 sites diffÃ©rents | | |
| Mot de passe root connu d'une seule personne | | |

---

## Exercice 5 : RÃ©flexion sur CrowdStrike

RÃ©pondez aux questions suivantes en quelques lignes :

**a) Pourquoi l'incident CrowdStrike illustre-t-il parfaitement le concept de SPOF ?**

_________________________________________________________________

_________________________________________________________________

**b) Quelle mesure aurait pu limiter l'impact de cet incident pour une organisation ?**

_________________________________________________________________

_________________________________________________________________

**c) Quel composant du SI (Laudon) Ã©tait Ã  l'origine du problÃ¨me ? Quels autres composants ont Ã©tÃ© impactÃ©s ?**

_________________________________________________________________

_________________________________________________________________

---

# CORRIGÃ‰ DES EXERCICES

## Exercice 1 : CorrigÃ©

| Ã‰lÃ©ment | Composant |
|---------|-----------|
| Un serveur Dell PowerEdge | **M** (MatÃ©riel) |
| La base de donnÃ©es clients | **D** (DonnÃ©es) |
| Le logiciel de comptabilitÃ© Sage | **L** (Logiciel) |
| La charte informatique de l'entreprise | **P** (ProcÃ©dures) |
| Le technicien rÃ©seau | **H** (Personnel) |
| Les sauvegardes quotidiennes | **D** (DonnÃ©es) |
| Le systÃ¨me d'exploitation Windows Server | **L** (Logiciel) |
| La procÃ©dure de gestion des mots de passe | **P** (ProcÃ©dures) |

---

## Exercice 2 : CorrigÃ©

**a)** 
- VulnÃ©rabilitÃ© : Personnel non sensibilisÃ© au phishing
- Menace : Email de phishing (attaquant)

**b)** 
- VulnÃ©rabilitÃ© : Serveur non mis Ã  jour
- Menace : Hacker exploitant la faille

**c)** 
- VulnÃ©rabilitÃ© : Sauvegardes sur le mÃªme site
- Menace : Incendie

---

## Exercice 3 : CorrigÃ© indicatif

| Situation | V | I | Risque | Niveau |
|-----------|---|---|--------|--------|
| Serveur de 10 ans hÃ©bergeant les donnÃ©es clients | 4 | 4 | 16 | ðŸ”´ CRITIQUE |
| Poste de travail avec antivirus Ã  jour | 2 | 1 | 2 | ðŸŸ¢ FAIBLE |
| Sauvegarde quotidienne testÃ©e mensuellement | 2 | 2 | 4 | ðŸŸ¡ MODÃ‰RÃ‰ |
| Mot de passe admin partagÃ© entre 5 personnes | 4 | 3 | 12 | ðŸ”´ CRITIQUE |
| WiFi ouvert aux visiteurs sans isolation rÃ©seau | 3 | 2 | 6 | ðŸŸ¡ MODÃ‰RÃ‰ |

---

## Exercice 4 : CorrigÃ©

| Ã‰lÃ©ment | SPOF ? | Solution |
|---------|--------|----------|
| Serveur unique hÃ©bergeant l'ERP | **OUI** | Serveur de secours ou cluster haute disponibilitÃ© |
| Deux liaisons Internet (Orange + SFR) | NON | Redondance dÃ©jÃ  en place |
| Technicien informatique unique | **OUI** | Formation d'un backup, documentation des procÃ©dures |
| Sauvegardes sur 3 sites diffÃ©rents | NON | Redondance suffisante |
| Mot de passe root connu d'une seule personne | **OUI** | Coffre-fort de mots de passe, partage sÃ©curisÃ© |

---

## Exercice 5 : Ã‰lÃ©ments de rÃ©ponse

**a)** CrowdStrike = SPOF car : logiciel unique, dÃ©ployÃ© partout, pas d'alternative, mise Ã  jour automatique sans contrÃ´le client.

**b)** Mesures possibles : dÃ©lai de dÃ©ploiement des mises Ã  jour, environnement de test, segmentation du parc, plan B sans CrowdStrike.

**c)** Origine : **Logiciel (L)**. Impacts : MatÃ©riel (Ã©cran bleu), DonnÃ©es (inaccessibles), ProcÃ©dures (bloquÃ©es), Personnel (inactif).

---



---

*BTS SIO - Bloc 3 - CybersÃ©curitÃ© et RÃ©silience - Support de cours SÃ©ance 1*
