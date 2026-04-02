# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a documentation repository containing the official French BTS FED (Brevet de Technicien Supérieur — Fluides Énergies Domotique) certification reference standard.

**Not a software project** — there is no build system, package manager, or test suite.

## Content Structure

```
Réferentiel_BTS_FED/
├── 3851-referentiel-bts-fed-mars14.md       # Full curriculum reference (542 KB Markdown)
├── 3851-referentiel-bts-fed-mars14_meta.json # Metadata for the document
└── _page_81_Figure_5.jpeg                    # Diagram image
```

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

## Fichiers à ne pas lire

- `Réferentiel_BTS_FED/` — référentiel source, ignoré après extraction initiale.
  Utiliser `context/gcf-recap.md` à la place pour tout contexte GCF.
- `cours/chapitres/*.tex` — ne lire que les fichiers explicitement indiqués dans `cours/state.md` sous `prochain_focus`.
