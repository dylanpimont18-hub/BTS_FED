# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a documentation repository containing the official French BTS FED (Brevet de Technicien Supérieur — Fluides Énergies Domotique) certification reference standard.

**Not a software project** — there is no build system, package manager, or test suite.

## Content Structure

```
context/
└── gcf-recap.md                              # Extracted GCF reference (~25 KB)

cours/
├── main.tex                                  # Fascicule 1 — Cours (bande FedBlue)
├── livret-exercices.tex                      # Fascicule 2 — Exercices (bande FedOrange)
├── livret-situations.tex                     # Fascicule 3 — Situations Réelles (bande FedGreen)
├── preamble.tex                              # Charte graphique commune aux 3 fascicules
├── state.md                                  # Suivi d'avancement + tâches agent automatisé
├── etudiant-bon.md / etudiant-mauvais.md / etudiant-tres-bon.md
├── chapitres/                                # 12 chapitres cours (00 à 11)
├── exercices/                                # 12 fichiers exercices (00 à 11)
└── situations/                               # 3 projets Situations Réelles
    ├── sr1-rehabilitation-maison.tex         # SR-1 Semestre 1 (ch01+02+04+05)
    ├── sr2-climatisation-tertiaire.tex       # SR-2 Semestre 2 (ch03+06+07+08)
    └── sr3-conception-immeuble.tex           # SR-3 Semestre 3 (ch00 à 11, transversal)
```

## Identité visuelle des 3 fascicules

| Fascicule | Fichier racine | Couleur bande | Public |
|-----------|---------------|---------------|--------|
| Référentiel de cours | `main.tex` | **FedBlue** `RGB(0,92,122)` | Cours magistral |
| Livret d'exercices | `livret-exercices.tex` | **FedOrange** `RGB(217,90,64)` | TD / Entraînement |
| Livret Situations Réelles | `livret-situations.tex` | **FedGreen** `RGB(74,124,89)` | Projets groupes |

## Document Scope

The main document covers the BTS FED diploma across three specializations:

- **Option GCF** — Génie climatique et fluidique (Climate & Fluid Engineering)
- **Option FCA** — Froid et conditionnement d'air (Refrigeration & Air Conditioning)
- **Option DBC** — Domotique et bâtiments communicants (Home Automation & Connected Buildings)

The document is structured around:
1. Professional activity descriptions (métiers)
2. Certification reference and competency frameworks
3. Training schedules and internship requirements
4. Exam procedures and assessment criteria

## Working with This Repository

All content is in French. The `.md` file was likely converted from a PDF — formatting may be imperfect in places due to the conversion process.

## Important Notes

- **Reference extraction complete** — Use `context/gcf-recap.md` for all GCF context.
- `cours/state.md` — Source de vérité pour l'état du cours. Contient la liste des tâches `TODO/EN_COURS/FAIT` pour l'agent automatisé.
- **Agent automatisé** — Un RemoteTrigger Anthropic exécute `.claude/commands/agent-auto.md` toutes les 5h. Il lit `state.md`, sélectionne 2 tâches `TODO` non conflictuelles, lance 2 sous-agents en parallèle, puis commite.
- **Jamais plus de 2 sous-agents simultanés** — Contrainte de quota Claude.
- `cours/chapitres/*.tex` — Ne lire que les fichiers indiqués dans `state.md` sous la colonne `Fichier cible` des tâches `EN_COURS`.
