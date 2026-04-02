# Design : Agent de génération de cours BTS FED — Option GCF

**Date :** 2026-04-02
**Auteur :** Dylan Pimont
**Statut :** Approuvé

---

## Contexte

Le dépôt `BTS_FED` contient le référentiel officiel du BTS Fluides Énergies Domotique (542 KB, Markdown). L'objectif est de créer un agent Claude Code qui génère et améliore en continu un cours complet de 2 ans, option GCF (Génie climatique et fluidique), pour une formation initiale. La sortie est un projet LaTeX compilable sur Overleaf via GitHub.

L'agent tourne toutes les 4h (aligné sur le reset des quotas de tokens) et améliore progressivement le cours existant plutôt que de tout régénérer.

---

## Architecture du dépôt

```
BTS_FED/
├── .claude/
│   └── commands/
│       ├── extract-gcf.md         # Commande /extract-gcf (run unique)
│       └── improve-cours.md       # Commande /improve-cours (run récurrent)
├── Réferentiel_BTS_FED/           # Ignoré par l'agent après extraction
├── context/
│   └── gcf-recap.md               # Extraction légère du référentiel GCF (~20-30 KB)
├── cours/
│   ├── state.md                   # Journal de progression de l'agent
│   ├── main.tex                   # Document maître (compilable sur Overleaf)
│   ├── preamble.tex               # Packages LaTeX, styles, macros communes
│   └── chapitres/
│       ├── 01-bases-thermiques.tex
│       ├── 02-hydraulique.tex
│       └── ...
├── docs/
│   └── superpowers/specs/
│       └── 2026-04-02-agent-cours-bts-fed-gcf-design.md
└── CLAUDE.md
```

---

## Commande `/extract-gcf` (run unique)

**Objectif :** Lire le référentiel complet une seule fois et produire `context/gcf-recap.md`.

**Ce que le recap contient :**
- Compétences GCF avec leurs niveaux de maîtrise (1 à 4)
- Savoirs associés à l'option GCF uniquement (hors FCA et DBC)
- Tâches professionnelles GCF
- Relations compétences ↔ savoirs

**Résultat attendu :** Réduction de 542 KB → ~20-30 KB de contexte utile.

**Après exécution :** Mettre à jour `CLAUDE.md` pour signaler que `Réferentiel_BTS_FED/` ne doit plus être lu — utiliser `context/gcf-recap.md` à la place.

---

## Commande `/improve-cours` (run récurrent, toutes les 4h)

### Cycle d'exécution

```
1. LIT  → context/gcf-recap.md       (~3-5k tokens)
2. LIT  → cours/state.md             (~1k tokens)
3. LIT  → 1-2 fichiers .tex cibles   (~3k tokens)
4. DÉCIDE → chapitre à créer ou améliorer
5. AGIT  → génère ou enrichit le .tex
6. MET À JOUR → cours/state.md
7. COMMIT → git commit avec message descriptif
```

**Budget tokens estimé par run : < 15k tokens**

### Logique de décision

L'agent consulte `cours/state.md` qui contient :
- La liste des chapitres avec leur statut : `ébauche` / `complet` / `révisé`
- Un score de qualité par chapitre (1 à 5)
- Un champ `prochain_focus` rédigé par l'agent à la fin du run précédent

**Priorités :**
1. Créer les chapitres manquants (statut absent)
2. Compléter les ébauches → `complet`
3. Enrichir les chapitres `complet` → `révisé` (exercices, exemples, approfondissements)

---

## Progression pédagogique GCF

Organisation du simple au complexe, indépendante de la progression semestrielle du référentiel :

| # | Chapitre | Niveau |
|---|----------|--------|
| 01 | Bases de la thermique (chaleur, transferts, enthalpie) | Fondamental |
| 02 | Hydraulique des circuits (débit, pertes de charge, pompes) | Fondamental |
| 03 | Aéraulique (réseaux de gaines, ventilation, CTA) | Fondamental |
| 04 | Production de chaleur (chaudières, PAC, solaire thermique) | Intermédiaire |
| 05 | Distribution et émission (radiateurs, plancher chauffant) | Intermédiaire |
| 06 | Climatisation et traitement d'air | Intermédiaire |
| 07 | Régulation et GTB | Avancé |
| 08 | Efficacité énergétique et RE2020 | Avancé |
| 09 | Acoustique du bâtiment | Avancé |
| 10 | Électrotechnique appliquée aux systèmes CVC | Avancé |
| 11 | Études de cas et dimensionnement complet | Synthèse |

### Structure type d'un chapitre LaTeX

```latex
\chapter{Titre}
  \section{Objectifs pédagogiques}   % liés aux compétences GCF
  \section{Cours}                    % théorie, formules, schémas
  \section{Exemples résolus}         % calculs chiffrés pas à pas
  \section{Exercices d'application}  % avec corrigés détaillés
  \section{Points réglementation}    % normes, RE2020, DTU associés
```

**Ton :** pédagogique mais professionnel — adapté à une formation initiale BTS.

---

## Optimisation des tokens

| Fichier | Taille | Rôle |
|---------|--------|------|
| `Réferentiel_BTS_FED/*.md` | 542 KB | Lu une seule fois par `/extract-gcf`, puis ignoré |
| `context/gcf-recap.md` | ~25 KB | Contexte de référence pour tous les runs |
| `cours/state.md` | < 2 KB | État courant, guide le prochain run |
| `cours/chapitres/*.tex` | 2-5 KB/ch | Lu 1-2 fichiers par run maximum |

**CLAUDE.md** sera mis à jour après l'extraction pour indiquer explicitement de ne pas lire `Réferentiel_BTS_FED/`.

---

## Contraintes techniques

- **LaTeX :** Structure `main.tex` + `\input{}` compatible Overleaf
- **Git :** L'agent commit après chaque amélioration avec un message explicite
- **Langue :** Cours en français, code LaTeX en anglais (noms de commandes)
- **Option :** GCF uniquement — aucun contenu FCA ou DBC
- **Public :** Étudiants en formation initiale BTS (pas d'alternance)
