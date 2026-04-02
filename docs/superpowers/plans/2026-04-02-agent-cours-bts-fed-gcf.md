# Agent BTS FED GCF — Cours LaTeX en amélioration continue

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Créer deux commandes Claude (`/extract-gcf` et `/improve-cours`) qui génèrent et améliorent en continu un cours BTS FED option GCF en LaTeX, optimisé pour un usage minimum de tokens.

**Architecture:** Une commande d'extraction unique lit le référentiel lourd (542 KB) et produit un récapitulatif GCF allégé (~25 KB). Une commande récurrente lit ce récapitulatif + un fichier d'état + 1-2 fichiers `.tex` cibles, améliore le cours, met à jour l'état et commite. Un cron local déclenche la commande récurrente toutes les 4h.

**Tech Stack:** Claude Code slash commands (Markdown), LaTeX (pdflatex/XeLaTeX), Git, cron local via CronCreate.

---

## Structure des fichiers

| Fichier | Action | Responsabilité |
|---------|--------|----------------|
| `.claude/commands/extract-gcf.md` | Créer | Prompt de la commande d'extraction unique |
| `.claude/commands/improve-cours.md` | Créer | Prompt de la commande d'amélioration récurrente |
| `context/gcf-recap.md` | Généré par `/extract-gcf` | Contexte GCF allégé (~25 KB) |
| `cours/state.md` | Créer + mis à jour par agent | Journal de progression (statuts, scores, focus) |
| `cours/main.tex` | Créer | Document maître Overleaf avec `\input{}` |
| `cours/preamble.tex` | Créer | Packages, styles, macros LaTeX |
| `cours/chapitres/*.tex` | Générés par agent | Un fichier par chapitre |
| `CLAUDE.md` | Modifier | Ajouter directive d'ignorer le référentiel lourd |

---

## Task 1 : Créer la structure de dossiers

**Files:**
- Create: `.claude/commands/` (dossier)
- Create: `context/` (dossier)
- Create: `cours/chapitres/` (dossier)

- [ ] **Step 1 : Créer les dossiers**

```bash
mkdir -p .claude/commands context cours/chapitres
```

- [ ] **Step 2 : Vérifier**

```bash
ls -la .claude/commands context cours/chapitres
```

Résultat attendu : 3 dossiers vides créés.

- [ ] **Step 3 : Commit**

```bash
git add .claude/ context/ cours/
git commit -m "chore: create project directory structure for BTS FED GCF agent"
```

---

## Task 2 : Créer la commande `/extract-gcf`

**Files:**
- Create: `.claude/commands/extract-gcf.md`

- [ ] **Step 1 : Créer le fichier de commande**

Créer `.claude/commands/extract-gcf.md` avec le contenu suivant :

```markdown
Lis le fichier `Réferentiel_BTS_FED/3851-referentiel-bts-fed-mars14.md` en entier.

Extrais UNIQUEMENT les éléments relatifs à l'option GCF (Génie climatique et fluidique).
Ignore tout contenu spécifique aux options FCA et DBC.

Produis le fichier `context/gcf-recap.md` avec cette structure exacte :

---

# Récapitulatif Référentiel BTS FED — Option GCF

## 1. Tâches professionnelles GCF
(Liste toutes les tâches avec leur code et niveau d'implication pour GCF)

## 2. Compétences GCF
(Pour chaque compétence : code, intitulé, niveau de maîtrise attendu 1-4, indicateurs de performance)

## 3. Savoirs associés GCF
(Pour chaque savoir : code, intitulé, contenu synthétisé, niveau d'acquisition 1-4)
(Ne garder que les savoirs mobilisés par les compétences GCF)

## 4. Relations compétences ↔ savoirs
(Tableau de correspondance : quelle compétence mobilise quels savoirs)

---

Contraintes :
- Objectif : fichier final < 30 KB
- Synthétise sans perdre la substance pédagogique
- Conserve les codes officiels (ex : C1.1, S1, T2.3...)
- Langue : français

Une fois `context/gcf-recap.md` créé, exécute :
```bash
git add context/gcf-recap.md
git commit -m "feat: extract GCF reference content from full referentiel"
```

Puis affiche : "Extraction terminée. Taille du recap : [taille réelle]"
```

- [ ] **Step 2 : Vérifier que la commande est accessible**

```bash
ls .claude/commands/extract-gcf.md
```

Résultat attendu : fichier présent.

- [ ] **Step 3 : Commit**

```bash
git add .claude/commands/extract-gcf.md
git commit -m "feat: add /extract-gcf slash command for one-time GCF extraction"
```

---

## Task 3 : Exécuter `/extract-gcf` et vérifier l'extraction

**Files:**
- Generated: `context/gcf-recap.md`

- [ ] **Step 1 : Lancer la commande**

Dans Claude Code, exécuter :
```
/extract-gcf
```

- [ ] **Step 2 : Vérifier la taille du fichier produit**

```bash
wc -c context/gcf-recap.md
```

Résultat attendu : entre 15 000 et 35 000 octets (15-35 KB). Si > 35 KB, relancer en demandant à Claude de synthétiser davantage.

- [ ] **Step 3 : Vérifier la structure du recap**

```bash
grep "^## " context/gcf-recap.md
```

Résultat attendu :
```
## 1. Tâches professionnelles GCF
## 2. Compétences GCF
## 3. Savoirs associés GCF
## 4. Relations compétences ↔ savoirs
```

- [ ] **Step 4 : Vérifier la présence des codes officiels**

```bash
grep -E "^### (C|S|T)[0-9]" context/gcf-recap.md | head -10
```

Résultat attendu : au moins 5 codes de compétences/savoirs listés.

---

## Task 4 : Mettre à jour CLAUDE.md

**Files:**
- Modify: `CLAUDE.md`

- [ ] **Step 1 : Ajouter la directive dans CLAUDE.md**

Ajouter à la fin de `CLAUDE.md` :

```markdown
## Fichiers à ne pas lire

- `Réferentiel_BTS_FED/` — référentiel source, ignoré après extraction initiale.
  Utiliser `context/gcf-recap.md` à la place pour tout contexte GCF.
- `cours/chapitres/*.tex` — ne lire que les fichiers explicitement indiqués dans `cours/state.md` sous `prochain_focus`.
```

- [ ] **Step 2 : Vérifier**

```bash
grep -A4 "Fichiers à ne pas lire" CLAUDE.md
```

Résultat attendu : les 3 directives apparaissent.

- [ ] **Step 3 : Commit**

```bash
git add CLAUDE.md
git commit -m "docs: update CLAUDE.md to ignore heavy referentiel after extraction"
```

---

## Task 5 : Créer le scaffold LaTeX

**Files:**
- Create: `cours/preamble.tex`
- Create: `cours/main.tex`

- [ ] **Step 1 : Créer `cours/preamble.tex`**

```latex
% preamble.tex — BTS FED GCF — Cours complet 2 ans
\usepackage[T1]{fontenc}
\usepackage[utf8]{inputenc}
\usepackage[french]{babel}
\usepackage{geometry}
\geometry{a4paper, margin=2.5cm}

% Mathématiques et unités
\usepackage{amsmath, amssymb, mathtools}
\usepackage{siunitx}
\sisetup{locale=FR, output-decimal-marker={,}}

% Tableaux et figures
\usepackage{booktabs, tabularx, multirow}
\usepackage{graphicx, float}
\usepackage{tikz}
\usetikzlibrary{shapes.geometric, arrows.meta, positioning}

% Mise en forme
\usepackage{xcolor}
\definecolor{btsprimary}{RGB}{0, 82, 147}
\definecolor{btssecondary}{RGB}{220, 237, 255}
\definecolor{btsaccent}{RGB}{255, 140, 0}

\usepackage{tcolorbox}
\tcbuselibrary{breakable, skins}

% Boîtes pédagogiques
\newtcolorbox{definition}[1][]{
  colback=btssecondary, colframe=btsprimary,
  fonttitle=\bfseries, title=Définition,#1
}
\newtcolorbox{methode}[1][]{
  colback=orange!10, colframe=btsaccent,
  fonttitle=\bfseries, title=Méthode,#1
}
\newtcolorbox{attention}[1][]{
  colback=red!8, colframe=red!60!black,
  fonttitle=\bfseries, title=Attention,#1
}
\newtcolorbox{exemple}[1][]{
  colback=green!8, colframe=green!50!black,
  fonttitle=\bfseries, title=Exemple résolu,#1
}

% En-têtes et pieds de page
\usepackage{fancyhdr}
\pagestyle{fancy}
\fancyhf{}
\fancyhead[L]{\small\textcolor{btsprimary}{BTS FED — Option GCF}}
\fancyhead[R]{\small\textcolor{btsprimary}{\leftmark}}
\fancyfoot[C]{\thepage}
\renewcommand{\headrulewidth}{0.4pt}

% Liens
\usepackage{hyperref}
\hypersetup{
  colorlinks=true, linkcolor=btsprimary,
  urlcolor=btsprimary, citecolor=btsprimary,
  pdftitle={Cours BTS FED — Option GCF},
  pdfauthor={Généré par agent Claude Code}
}

% Numérotation des exercices
\newcounter{exercice}[chapter]
\newcommand{\exercice}[1]{%
  \stepcounter{exercice}%
  \subsection*{Exercice \theexercice\ — #1}%
}
```

- [ ] **Step 2 : Créer `cours/main.tex`**

```latex
\documentclass[12pt, a4paper, twoside]{report}
\input{preamble}

\begin{document}

\begin{titlepage}
  \centering
  \vspace*{3cm}
  {\Huge\bfseries\textcolor{btsprimary}{BTS FED}\par}
  \vspace{0.5cm}
  {\Large Option Génie Climatique et Fluidique\par}
  \vspace{1cm}
  \rule{\linewidth}{0.5pt}
  \vspace{0.5cm}
  {\LARGE\bfseries Cours complet — Formation 2 ans\par}
  \vspace{0.5cm}
  \rule{\linewidth}{0.5pt}
  \vspace{2cm}
  {\large Formation initiale\par}
  \vspace{0.5cm}
  {\large\textit{Généré et amélioré en continu par agent Claude Code}\par}
  \vfill
  {\large \today\par}
\end{titlepage}

\tableofcontents
\newpage

% Chapitres — générés et \input{} ajoutés progressivement par l'agent
% \input{chapitres/01-bases-thermiques}
% \input{chapitres/02-hydraulique}
% \input{chapitres/03-aeraulique}
% \input{chapitres/04-production-chaleur}
% \input{chapitres/05-distribution-emission}
% \input{chapitres/06-climatisation}
% \input{chapitres/07-regulation-gtb}
% \input{chapitres/08-efficacite-energetique}
% \input{chapitres/09-acoustique}
% \input{chapitres/10-electrotechnique}
% \input{chapitres/11-etudes-de-cas}

\end{document}
```

- [ ] **Step 3 : Commit**

```bash
git add cours/main.tex cours/preamble.tex
git commit -m "feat: add LaTeX scaffold (main.tex + preamble) for BTS FED GCF cours"
```

---

## Task 6 : Créer `cours/state.md`

**Files:**
- Create: `cours/state.md`

- [ ] **Step 1 : Créer le fichier d'état initial**

Créer `cours/state.md` avec le contenu suivant :

```markdown
# État du cours BTS FED GCF

Mis à jour automatiquement par l'agent à chaque run.

## Dernier run
- Date : (premier run à venir)
- Action : initialisation

## Prochain focus
Créer le chapitre 01 : Bases de la thermique.
Fichier cible : `cours/chapitres/01-bases-thermiques.tex`
Objectif : ébauche complète avec cours, 2 exemples résolus, 3 exercices.

## Chapitres

| # | Fichier | Titre | Statut | Score /5 | Notes |
|---|---------|-------|--------|----------|-------|
| 01 | 01-bases-thermiques.tex | Bases de la thermique | absent | — | À créer en priorité |
| 02 | 02-hydraulique.tex | Hydraulique des circuits | absent | — | |
| 03 | 03-aeraulique.tex | Aéraulique | absent | — | |
| 04 | 04-production-chaleur.tex | Production de chaleur | absent | — | |
| 05 | 05-distribution-emission.tex | Distribution et émission | absent | — | |
| 06 | 06-climatisation.tex | Climatisation et traitement d'air | absent | — | |
| 07 | 07-regulation-gtb.tex | Régulation et GTB | absent | — | |
| 08 | 08-efficacite-energetique.tex | Efficacité énergétique et RE2020 | absent | — | |
| 09 | 09-acoustique.tex | Acoustique du bâtiment | absent | — | |
| 10 | 10-electrotechnique.tex | Électrotechnique appliquée CVC | absent | — | |
| 11 | 11-etudes-de-cas.tex | Études de cas et dimensionnement | absent | — | |

## Légende des statuts
- `absent` : chapitre non encore créé
- `ébauche` : structure créée, contenu partiel
- `complet` : cours + exemples + exercices présents
- `révisé` : relu, enrichi, exercices corrigés complets
```

- [ ] **Step 2 : Commit**

```bash
git add cours/state.md
git commit -m "feat: add initial cours/state.md for agent progression tracking"
```

---

## Task 7 : Créer la commande `/improve-cours`

**Files:**
- Create: `.claude/commands/improve-cours.md`

- [ ] **Step 1 : Créer `.claude/commands/improve-cours.md`**

```markdown
Tu es un enseignant expert en génie climatique et fluidique (GCF), chargé d'améliorer un cours BTS FED de haute qualité.

## Étape 1 — Charger le contexte (ne lis QUE ces fichiers)

1. Lis `context/gcf-recap.md` — référentiel GCF allégé (compétences, savoirs, tâches)
2. Lis `cours/state.md` — état courant du cours et prochain focus

## Étape 2 — Décider l'action

Applique ces priorités dans l'ordre :
1. Si des chapitres ont le statut `absent` → créer le premier de la liste
2. Si des chapitres ont le statut `ébauche` → compléter le premier de la liste
3. Si des chapitres ont le statut `complet` → enrichir celui avec le score le plus bas
4. Sinon → améliorer le chapitre `révisé` avec le score le plus bas

Lis le fichier `.tex` cible indiqué dans `prochain_focus` (ou crée-le s'il est absent).
Ne lis pas d'autres fichiers `.tex`.

## Étape 3 — Générer ou améliorer le chapitre

### Pour un chapitre `absent` → créer une `ébauche`

Génère un fichier `.tex` complet avec cette structure :

```latex
\chapter{[Titre du chapitre]}

\section{Objectifs pédagogiques}
% Liste des compétences GCF mobilisées (codes du recap)
% Liste des savoirs associés mobilisés (codes du recap)

\section{Introduction}
% Mise en contexte professionnelle (1 paragraphe)

\section{[Contenu théorique section 1]}
% Cours avec formules numérotées (\begin{equation}...\end{equation})
% Utiliser les boîtes : \begin{definition}...\end{definition}
%                       \begin{methode}...\end{methode}
%                       \begin{attention}...\end{attention}

\section{Exemples résolus}
\begin{exemple}
  % Énoncé + résolution pas à pas avec valeurs numériques réelles
\end{exemple}

\section{Exercices d'application}
\exercice{[Titre]}
% Énoncé complet avec données numériques

\section{Éléments de réglementation}
% DTU, normes EN/NF, RE2020 associés au chapitre
```

### Pour un chapitre `ébauche` → compléter vers `complet`

- Compléter toutes les sections théoriques manquantes
- Ajouter au moins 2 exemples résolus chiffrés
- Ajouter au moins 3 exercices avec corrigés détaillés
- Vérifier la cohérence des formules

### Pour un chapitre `complet` ou `révisé` → enrichir

- Approfondir un point identifié comme superficiel
- Ajouter un exemple issu d'un cas terrain réel
- Améliorer la clarté pédagogique
- Ajouter ou améliorer les corrigés des exercices

## Contraintes de qualité

- **Ton :** pédagogique mais professionnel — ni trop scolaire, ni trop académique
- **Formules :** toujours avec unités SI, variables expliquées
- **Exemples :** valeurs numériques réalistes issues du secteur CVC français
- **Réglementation :** mentionner DTU, normes NF EN, RE2020 quand pertinent
- **LaTeX :** utiliser les boîtes définies dans preamble.tex (definition, methode, attention, exemple)
- **Langue :** français intégral, terminologie professionnelle correcte

## Étape 4 — Mettre à jour `cours/state.md`

Mets à jour :
- La ligne du chapitre traité (nouveau statut, nouveau score /5)
- `Dernier run` (date du jour et action effectuée)
- `Prochain focus` (quel chapitre traiter au prochain run et pourquoi)

## Étape 5 — Mettre à jour `cours/main.tex`

Si le chapitre vient d'être créé, décommenter la ligne `\input{chapitres/...}` correspondante dans `cours/main.tex`.

## Étape 6 — Commiter

```bash
git add cours/chapitres/[fichier-modifié].tex cours/state.md cours/main.tex
git commit -m "cours(gcf): [action] chapitre [N] — [titre court]"
```

Puis affiche un résumé : chapitre traité, action effectuée, score attribué, prochain focus prévu.
```

- [ ] **Step 2 : Vérifier la présence du fichier**

```bash
ls .claude/commands/improve-cours.md
```

Résultat attendu : fichier présent.

- [ ] **Step 3 : Commit**

```bash
git add .claude/commands/improve-cours.md
git commit -m "feat: add /improve-cours recurring slash command for continuous course improvement"
```

---

## Task 8 : Premier run de `/improve-cours`

**Files:**
- Generated: `cours/chapitres/01-bases-thermiques.tex`
- Modified: `cours/state.md`, `cours/main.tex`

- [ ] **Step 1 : Lancer la commande**

Dans Claude Code, exécuter :
```
/improve-cours
```

- [ ] **Step 2 : Vérifier que le chapitre 01 a été créé**

```bash
ls cours/chapitres/
```

Résultat attendu : `01-bases-thermiques.tex` présent.

- [ ] **Step 3 : Vérifier la structure du chapitre**

```bash
grep "^\\\\section" cours/chapitres/01-bases-thermiques.tex
```

Résultat attendu : au moins 4 sections (Objectifs, Introduction, [contenu], Exemples, Exercices, Réglementation).

- [ ] **Step 4 : Vérifier la mise à jour de state.md**

```bash
grep "01-bases-thermiques" cours/state.md
```

Résultat attendu : statut différent de `absent` (devrait être `ébauche`).

- [ ] **Step 5 : Vérifier que main.tex a été mis à jour**

```bash
grep "input{chapitres/01" cours/main.tex
```

Résultat attendu : ligne décommentée (`\input{chapitres/01-bases-thermiques}`).

---

## Task 9 : Configurer le cron local (toutes les 4h)

- [ ] **Step 1 : Identifier le chemin du projet**

```bash
pwd
```

Note le chemin absolu du repo (ex. `/c/Users/Dylan/Desktop/Creation_site/BTS_FED`).

- [ ] **Step 2 : Créer le cron via CronCreate**

Utiliser l'outil `CronCreate` avec les paramètres suivants :
- **Schedule :** `0 */4 * * *` (toutes les 4 heures)
- **Command :** `claude --dangerously-skip-permissions /improve-cours`
- **Working directory :** chemin absolu du repo BTS_FED
- **Description :** "Amélioration continue cours BTS FED GCF"

- [ ] **Step 3 : Vérifier le cron créé**

Utiliser `CronList` pour confirmer que le cron apparaît avec le bon schedule.

- [ ] **Step 4 : Commit final**

```bash
git add .
git status
git commit -m "feat: complete BTS FED GCF agent setup — ready for continuous improvement"
```

---

## Self-Review

**Couverture spec :**
- ✅ Extraction unique → Task 2 + Task 3
- ✅ Token budget optimisé → Task 4 (CLAUDE.md), commande `/improve-cours` lit max 3 fichiers
- ✅ LaTeX + Overleaf → Task 5
- ✅ state.md → Task 6
- ✅ `/improve-cours` récurrent → Task 7 + Task 8
- ✅ Cron 4h → Task 9
- ✅ GCF uniquement → commandes filtrées sur GCF
- ✅ Formation initiale → ton défini dans `/improve-cours`
- ✅ Progression pédagogique propre → state.md liste 11 chapitres dans l'ordre logique

**Aucun placeholder détecté.** Chaque step contient le contenu réel ou la commande exacte.

**Cohérence :** Les noms de fichiers `.tex` dans state.md, main.tex et les commandes sont identiques.
