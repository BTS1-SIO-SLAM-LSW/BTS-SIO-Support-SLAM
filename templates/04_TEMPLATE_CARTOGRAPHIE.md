# CARTOGRAPHIE DES RISQUES 
## Méthode EBIOS simplifiée + Classification OWASP + Analyse SPOF

**Binôme : _________________________ | Date : _______________**

---

# RAPPELS MÉTHODOLOGIQUES

## Formule du risque

```
┌────────────────────────────────────────────┐
│   RISQUE = VRAISEMBLANCE (V) × IMPACT (I)  │
└────────────────────────────────────────────┘
```

## Échelle de vraisemblance (V)

| Niveau | Libellé | Description | Contexte SLAM |
|--------|---------|-------------|---------------|
| **1** | Très improbable | Moyens exceptionnels | Faille 0-day complexe |
| **2** | Peu probable | Compétences particulières | Attaque ciblée |
| **3** | Probable | Outils disponibles | SQLmap, Burp Suite |
| **4** | Très probable | Exploitation triviale | Faille documentée, copier-coller |

## Échelle d'impact (I)

| Niveau | Libellé | Impact technique | Impact métier |
|--------|---------|------------------|---------------|
| **1** | Mineur | Info disclosure limitée | Pas d'impact client |
| **2** | Significatif | Accès partiel données | Quelques clients impactés |
| **3** | Grave | Compromission système | Fuite données clients |
| **4** | Critique | Compromission totale | Arrêt d'activité, RGPD |

## Matrice de criticité EBIOS

| V \ I | Impact 1 | Impact 2 | Impact 3 | Impact 4 |
|-------|----------|----------|----------|----------|
| **V = 4** | 4 🟡 MODÉRÉ | 8 🟠 ÉLEVÉ | 12 🔴 CRITIQUE | 16 🔴 CRITIQUE |
| **V = 3** | 3 🟢 FAIBLE | 6 🟡 MODÉRÉ | 9 🟠 ÉLEVÉ | 12 🔴 CRITIQUE |
| **V = 2** | 2 🟢 FAIBLE | 4 🟡 MODÉRÉ | 6 🟡 MODÉRÉ | 8 🟠 ÉLEVÉ |
| **V = 1** | 1 🟢 FAIBLE | 2 🟢 FAIBLE | 3 🟢 FAIBLE | 4 🟡 MODÉRÉ |

## Niveaux d'action

| Niveau | Score | Couleur | Action requise | Délai |
|--------|-------|---------|----------------|-------|
| **CRITIQUE** | 12-16 | 🔴 | Arrêt et correction immédiate | < 24-48h |
| **ÉLEVÉ** | 8-11 | 🟠 | Sprint dédié sécurité | < 1 mois |
| **MODÉRÉ** | 4-7 | 🟡 | Backlog priorisé | < 3-6 mois |
| **FAIBLE** | 1-3 | 🟢 | Amélioration continue | Prochain cycle |

---

# PARTIE 1 : VULNÉRABILITÉS APPLICATIVES (CODE)

## A01 — Broken Access Control

| Réf. | Vulnérabilité | Fichier/Ligne | V | I | Risque | Niveau | Correction |
|------|---------------|---------------|---|---|--------|--------|------------|
| A01-1 | | | | | | | |
| A01-2 | | | | | | | |

## A02 — Cryptographic Failures

| Réf. | Vulnérabilité | Fichier/Ligne | V | I | Risque | Niveau | Correction |
|------|---------------|---------------|---|---|--------|--------|------------|
| A02-1 | | | | | | | |
| A02-2 | | | | | | | |
| A02-3 | | | | | | | |

## A03 — Injection (SQL, NoSQL, XSS)

| Réf. | Vulnérabilité | Fichier/Ligne | V | I | Risque | Niveau | Correction |
|------|---------------|---------------|---|---|--------|--------|------------|
| A03-1 | | | | | | | |
| A03-2 | | | | | | | |
| A03-3 | | | | | | | |

## A05 — Security Misconfiguration

| Réf. | Vulnérabilité | Fichier/Ligne | V | I | Risque | Niveau | Correction |
|------|---------------|---------------|---|---|--------|--------|------------|
| A05-1 | | | | | | | |
| A05-2 | | | | | | | |

## A06 — Vulnerable Components

| Réf. | Vulnérabilité | Composant | V | I | Risque | Niveau | Correction |
|------|---------------|-----------|---|---|--------|--------|------------|
| A06-1 | | | | | | | |
| A06-2 | | | | | | | |

## A07 — Authentication Failures

| Réf. | Vulnérabilité | Fichier/Ligne | V | I | Risque | Niveau | Correction |
|------|---------------|---------------|---|---|--------|--------|------------|
| A07-1 | | | | | | | |
| A07-2 | | | | | | | |

## A09 — Logging & Monitoring Failures

| Réf. | Vulnérabilité | Fichier/Ligne | V | I | Risque | Niveau | Correction |
|------|---------------|---------------|---|---|--------|--------|------------|
| A09-1 | | | | | | | |

---

# PARTIE 2 : VULNÉRABILITÉS INFRASTRUCTURE (LAUDON)

## Composant M — Matériel / Cloud

| Réf. | Vulnérabilité | Menace | V | I | Risque | Niveau |
|------|---------------|--------|---|---|--------|--------|
| M1 | | | | | | |
| M2 | | | | | | |

## Composant L — Logiciel (hors code applicatif)

| Réf. | Vulnérabilité | Menace | V | I | Risque | Niveau |
|------|---------------|--------|---|---|--------|--------|
| L1 | | | | | | |
| L2 | | | | | | |

## Composant D — Données

| Réf. | Vulnérabilité | Menace | V | I | Risque | Niveau |
|------|---------------|--------|---|---|--------|--------|
| D1 | | | | | | |
| D2 | | | | | | |
| D3 | | | | | | |

## Composant P — Procédures / DevOps

| Réf. | Vulnérabilité | Menace | V | I | Risque | Niveau |
|------|---------------|--------|---|---|--------|--------|
| P1 | | | | | | |
| P2 | | | | | | |
| P3 | | | | | | |

## Composant H — Personnel

| Réf. | Vulnérabilité | Menace | V | I | Risque | Niveau |
|------|---------------|--------|---|---|--------|--------|
| H1 | | | | | | |
| H2 | | | | | | |

---

# PARTIE 3 : ANALYSE DES SPOF

> **SPOF** = Single Point of Failure = Point unique de défaillance
> « Si cet élément tombe, tout s'arrête »

| # | Type | Élément SPOF | Impact si défaillance | V | I | Risque | Solution |
|---|------|--------------|----------------------|---|---|--------|----------|
| SPOF1 | ☐ M ☐ L ☐ D ☐ P ☐ H | | | | | | |
| SPOF2 | ☐ M ☐ L ☐ D ☐ P ☐ H | | | | | | |
| SPOF3 | ☐ M ☐ L ☐ D ☐ P ☐ H | | | | | | |
| SPOF4 | ☐ M ☐ L ☐ D ☐ P ☐ H | | | | | | |
| SPOF5 | ☐ M ☐ L ☐ D ☐ P ☐ H | | | | | | |

---

# PARTIE 4 : ANALYSE DE RÉSILIENCE

## Indicateurs RTO / RPO

| Indicateur | Définition | Valeur actuelle DevSecure | Valeur recommandée |
|------------|------------|---------------------------|-------------------|
| **RTO** | Durée max d'interruption acceptable | | |
| **RPO** | Perte de données max acceptable | | |

## État des 4 piliers de la résilience

| Pilier | Description | État DevSecure | Actions nécessaires |
|--------|-------------|----------------|---------------------|
| **ANTICIPER** | Identifier les risques avant | ☐ ❌ ☐ ⚠️ ☐ ✅ | |
| **RÉSISTER** | Limiter l'impact | ☐ ❌ ☐ ⚠️ ☐ ✅ | |
| **ABSORBER** | Maintenir les fonctions essentielles | ☐ ❌ ☐ ⚠️ ☐ ✅ | |
| **SE RÉTABLIR** | Revenir à la normale | ☐ ❌ ☐ ⚠️ ☐ ✅ | |

## Conformité réglementaire

| Réglementation | Concerné ? | Conforme ? | Actions |
|----------------|------------|------------|---------|
| **RGPD** | ☐ Oui ☐ Non | ☐ Oui ☐ Non | |
| **NIS2** | ☐ Oui ☐ Non | ☐ Oui ☐ Non | |

---

# SYNTHÈSE DES RISQUES

## Risques CRITIQUES (12-16) 🔴 — Action immédiate

| Rang | Réf. | Vulnérabilité | Risque | Correction prioritaire |
|------|------|---------------|--------|------------------------|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |

## Risques ÉLEVÉS (8-11) 🟠 — Action sous 1 mois

| Rang | Réf. | Vulnérabilité | Risque | Correction planifiée |
|------|------|---------------|--------|----------------------|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |

---

# STATISTIQUES

| Indicateur | Valeur |
|------------|--------|
| **Total vulnérabilités CODE (OWASP)** | |
| **Total vulnérabilités INFRA (Laudon)** | |
| **Total SPOF** | |
| **TOTAL GÉNÉRAL** | |
| Risques 🔴 CRITIQUES | |
| Risques 🟠 ÉLEVÉS | |
| Risques 🟡 MODÉRÉS | |
| Risques 🟢 FAIBLES | |
| Catégorie OWASP la plus représentée | |
| Composant Laudon le plus vulnérable | |
| Score de risque moyen | |

---

# PLAN DE REMÉDIATION

## Quick Wins (< 1 jour)

| # | Correction | Réf. | Impact sécurité |
|---|------------|------|-----------------|
| 1 | | | |
| 2 | | | |
| 3 | | | |

## Corrections moyennes (1-5 jours)

| # | Correction | Réf. | Impact sécurité |
|---|------------|------|-----------------|
| 1 | | | |
| 2 | | | |

## Chantiers majeurs (> 5 jours)

| # | Correction | Réf. | Impact sécurité |
|---|------------|------|-----------------|
| 1 | | | |
| 2 | | | |

---

# AUTO-ÉVALUATION

| Critère | Validé |
|---------|--------|
| J'ai identifié au moins 8 vulnérabilités CODE (OWASP) | ☐ Oui ☐ Non |
| J'ai couvert au moins 4 catégories OWASP | ☐ Oui ☐ Non |
| J'ai identifié au moins 7 vulnérabilités INFRA (Laudon) | ☐ Oui ☐ Non |
| J'ai couvert les 5 composants Laudon (MLDPP) | ☐ Oui ☐ Non |
| J'ai identifié au moins 3 SPOF | ☐ Oui ☐ Non |
| J'ai défini RTO et RPO pour DevSecure | ☐ Oui ☐ Non |
| J'ai proposé des corrections pour les risques critiques | ☐ Oui ☐ Non |
| **Total ≥ 15 vulnérabilités** | ☐ Oui ☐ Non |

---

*Document étudiant SLAM — Version standard — Séance 1 — BTS SIO Bloc 3*
