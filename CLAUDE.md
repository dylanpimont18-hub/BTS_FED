# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a documentation repository containing the official French BTS FED (Brevet de Technicien Supérieur — Fluides Énergies Domotique) certification reference standard.

**Not a software project** — there is no build system, package manager, or test suite.

## Content Structure

```
context/
├── gcf-recap.md                              # Extracted GCF reference (~25 KB)
└── .gitkeep

cours/
├── main.tex, preamble.tex, livret-exercices.tex
├── state.md                                  # Agent progress tracking
├── chapitres/                                # 11 course chapters (LaTeX)
└── exercices/                                # Exercise files (LaTeX)
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

## Important Notes

- **Reference extraction complete** — The original 542 KB Réferentiel_BTS_FED has been extracted and archived. Use `context/gcf-recap.md` for all GCF context.
- `cours/chapitres/*.tex` — Only read files explicitly indicated in [cours/state.md](cours/state.md#L15) under `prochain_focus`.
