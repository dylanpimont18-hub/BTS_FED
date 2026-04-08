# État du cours BTS FED GCF

Mis à jour automatiquement par l'agent à chaque run.
**Format de suivi machine :** chaque section est parsée par l'agent automatisé.

---

## Dernier run
- Date : 2026-04-08 (11ème run)
- Action : **T11 — Fiche mémo tcolorbox ajoutée en fin de ch07 (regulation-gtb.tex, 5 formules clés : correcteur P, correcteur PID, loi d'eau, démarrage optimal, puissance PAC + tableau niveaux GTB) | T12 — Fiche mémo tcolorbox ajoutée en fin de ch08 (efficacite-energetique.tex, 7 formules clés : Bbio, Cep, Cep,nr, COP/SCOP PAC, rendement récupération double flux, consommation chauffage réglementaire, besoin chauffage DJU)**

---

## Prochain focus — Tâches pour l'agent automatisé

> L'agent lit ce bloc et choisit les 2 premières tâches avec statut `TODO` et fichiers non conflictuels.

| ID | Priorité | Statut | Fichier cible | Description |
|----|----------|--------|---------------|-------------|
| T01 | HAUTE | **FAIT** | `cours/livret-exercices.tex` | Ajouter `\input` manquants ch01-07 dans le livret |
| T02 | HAUTE | **FAIT** | `cours/etudiant-mauvais.md` | Rédiger profil pédagogique étudiant en difficulté |
| T03 | HAUTE | **FAIT** | `cours/etudiant-bon.md` | Rédiger profil pédagogique étudiant dans la moyenne |
| T04 | HAUTE | **FAIT** | `cours/etudiant-tres-bon.md` | Rédiger profil pédagogique étudiant excellent |
| T05 | MOYENNE | **FAIT** | `cours/chapitres/01-bases-thermiques.tex` | Ajouter fiche mémo fin de chapitre (boîte tcolorbox récap formules) |
| T06 | MOYENNE | **FAIT** | `cours/chapitres/02-hydraulique.tex` | Ajouter fiche mémo fin de chapitre |
| T07 | MOYENNE | **FAIT** | `cours/chapitres/03-aeraulique.tex` | Ajouter fiche mémo fin de chapitre |
| T08 | MOYENNE | **FAIT** | `cours/chapitres/04-production-chaleur.tex` | Ajouter fiche mémo fin de chapitre |
| T09 | MOYENNE | **FAIT** | `cours/chapitres/05-distribution-emission.tex` | Ajouter fiche mémo fin de chapitre |
| T10 | MOYENNE | **FAIT** | `cours/chapitres/06-climatisation.tex` | Ajouter fiche mémo fin de chapitre |
| T11 | MOYENNE | **FAIT** | `cours/chapitres/07-regulation-gtb.tex` | Ajouter fiche mémo fin de chapitre |
| T12 | MOYENNE | **FAIT** | `cours/chapitres/08-efficacite-energetique.tex` | Ajouter fiche mémo fin de chapitre |
| T13 | MOYENNE | **TODO** | `cours/chapitres/09-acoustique.tex` | Ajouter fiche mémo fin de chapitre |
| T14 | MOYENNE | **TODO** | `cours/chapitres/10-electrotechnique.tex` | Ajouter fiche mémo fin de chapitre |
| T15 | FAIBLE | **TODO** | `cours/chapitres/00-analyse-dimensionnelle.tex` | Enrichir avec données terrain réelles (catalogues Grundfos, Daikin) |
| T16 | FAIBLE | **TODO** | `cours/chapitres/11-etudes-de-cas.tex` | Ajouter renvois inter-chapitres explicites |
| T17 | FAIBLE | **TODO** | `cours/preamble.tex` | Ajouter environnement `fichemémo` (tcolorbox récap formules) |

### Règles de sélection des tâches
```
1. Prendre les 2 premières tâches TODO de priorité HAUTE en premier
2. Si moins de 2 HAUTE disponibles, compléter avec MOYENNE
3. Jamais 2 tâches sur le même fichier simultanément
4. Marquer la tâche EN_COURS pendant l'exécution, puis FAIT à la fin
5. Mettre à jour ce fichier state.md après chaque run
```

---

## Fascicules — État global

| Fascicule | Fichier | Couleur | Statut | Compilation |
|-----------|---------|---------|--------|-------------|
| Référentiel de cours | `main.tex` | FedBlue | ✅ Complet | Non testée (LaTeX requis) |
| Livret d'exercices | `livret-exercices.tex` | FedOrange | ✅ Complet (ch00-11) | Non testée |
| Livret Situations Réelles | `livret-situations.tex` | FedGreen | ✅ Créé (3 SR) | Non testée |

---

## Chapitres — Référentiel de cours (`main.tex`)

| # | Fichier | Titre | Statut | Score /5 | Notes |
|---|---------|-------|--------|----------|-------|
| 00 | 00-analyse-dimensionnelle.tex | Analyse dimensionnelle | révisé | 5 | TikZ ✅ \finchapitre ✅ |
| 01 | 01-bases-thermiques.tex | Bases de la thermique | révisé | 5 | TikZ ✅ \finchapitre ✅ |
| 02 | 02-hydraulique.tex | Hydraulique des circuits | révisé | 5 | TikZ ✅ \finchapitre ✅ |
| 03 | 03-aeraulique.tex | Aéraulique | révisé | 5 | TikZ ✅ \finchapitre ✅ |
| 04 | 04-production-chaleur.tex | Production de chaleur | révisé | 5 | TikZ ✅ \finchapitre ✅ |
| 05 | 05-distribution-emission.tex | Distribution et émission | révisé | 5 | TikZ ✅ \finchapitre ✅ |
| 06 | 06-climatisation.tex | Climatisation | révisé | 5 | TikZ ✅ \finchapitre ✅ |
| 07 | 07-regulation-gtb.tex | Régulation et GTB | révisé | 5 | TikZ ✅ \finchapitre ✅ |
| 08 | 08-efficacite-energetique.tex | Efficacité énergétique | révisé | 5 | TikZ ✅ \finchapitre ✅ |
| 09 | 09-acoustique.tex | Acoustique | révisé | 5 | TikZ ✅ \finchapitre ✅ |
| 10 | 10-electrotechnique.tex | Électrotechnique | révisé | 5 | TikZ ✅ \finchapitre ✅ |
| 11 | 11-etudes-de-cas.tex | Études de cas | révisé | 5 | TikZ ✅ \finchapitre ✅ |

## Exercices (`livret-exercices.tex`)

| # | Fichier | Inclus dans livret | Statut |
|---|---------|-------------------|--------|
| 00 | exercices/00-exercices.tex | ✅ Oui | complet |
| 01 | exercices/01-exercices.tex | ✅ Oui | complet |
| 02 | exercices/02-exercices.tex | ✅ Oui | complet |
| 03 | exercices/03-exercices.tex | ✅ Oui | complet |
| 04 | exercices/04-exercices.tex | ✅ Oui | complet |
| 05 | exercices/05-exercices.tex | ✅ Oui | complet |
| 06 | exercices/06-exercices.tex | ✅ Oui | complet |
| 07 | exercices/07-exercices.tex | ✅ Oui | complet |
| 08 | exercices/08-exercices.tex | ✅ Oui | complet |
| 09 | exercices/09-exercices.tex | ✅ Oui | complet |
| 10 | exercices/10-exercices.tex | ✅ Oui | complet |
| 11 | exercices/11-exercices.tex | ✅ Oui | complet |

## Situations Réelles (`livret-situations.tex`)

| # | Fichier | Titre | Semestre | Statut | TikZ |
|---|---------|-------|----------|--------|------|
| SR-1 | situations/sr1-rehabilitation-maison.tex | Réhabilitation maison | S1 | ✅ Créé | 2 schémas |
| SR-2 | situations/sr2-climatisation-tertiaire.tex | Tertiaire CTA+GTB | S2 | ✅ Créé | 2 schémas |
| SR-3 | situations/sr3-conception-immeuble.tex | Immeuble R+4 | S3 | ✅ Créé | 2 schémas |

## Profils étudiants

| Fichier | Statut |
|---------|--------|
| etudiant-mauvais.md | ✅ Rédigé (T02 FAIT) |
| etudiant-bon.md | ✅ Rédigé (T03 FAIT) |
| etudiant-tres-bon.md | ✅ Rédigé (T04 FAIT) |

---

## Légende des statuts
- `absent` : non encore créé
- `ébauche` : structure créée, contenu partiel
- `complet` : cours + exemples + exercices présents
- `révisé` : relu, enrichi, diagrammes TikZ, exercices corrigés complets
- `TODO` / `EN_COURS` / `FAIT` : suivi des tâches agent automatisé
