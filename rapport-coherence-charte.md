# Audit de Cohérence — Charte Graphique BTS FED

**Date:** 7 avril 2026  
**Analyse de:** preamble.tex, main.tex, livret-exercices.tex, chapitres/00-analyse-dimensionnelle.tex, chapitres/01-bases-thermiques.tex, chapitres/11-etudes-de-cas.tex, exercices/00-exercices.tex

---

## 🔴 PROBLÈMES CRITIQUES (bloquants)

### 1. **Erreur dans le preamble : Couleurs "bts*" non définies**

**Gravité:** 🔴 CRITIQUE — Les fichiers ne peuvent pas compiler correctement

**Location:** [preamble.tex](preamble.tex) lignes 150-180 (fin du fichier)

**Problème:**
- Les couleurs **`btsprimary`**, **`btsaccent`**, **`btsrule`** sont utilisées MAIS **jamais définies**
- Elles appear dans:
  - `titleformat` (sections, subsections) — ligne ~133-148
  - `tocloft` (table des matières) — ligne ~150-155
  - `fancyhdr` (en-têtes/pieds) — ligne ~160-170
  - `hyperref` (liens hypertextes) — ligne ~175

**Contraste avec le début du preamble:**
- Lignes 30-35 **définissent correctement** les 5 couleurs FED:
  ```latex
  \definecolor{FedBlue}{RGB}{0, 92, 122}
  \definecolor{FedOrange}{RGB}{217, 90, 64}
  \definecolor{FedGreen}{RGB}{74, 124, 89}
  \definecolor{FedRed}{RGB}{192, 57, 43}
  \definecolor{FedExercice}{RGB}{44, 62, 80}
  ```

**Résultat:**
- Les éléments tcolorbox en début de preamble sont correctement définis (✓)
- Mais tous les styles de titre, en-têtes, table des matières, liens tentent d'utiliser des couleurs inexistantes ❌

**Que devrait-il y avoir:**
```latex
% Après les définitions de couleur FED (ligne 35):
\definecolor{btsprimary}{RGB}{0, 92, 122}      % ← alias pour FedBlue
\definecolor{btsaccent}{RGB}{217, 90, 64}       % ← alias pour FedOrange
\definecolor{btsrule}{RGB}{0, 92, 122}          % ← alias pour FedBlue
```

---

### 2. **Preamble dupliqué/contradictoire — deux en-tête systems**

**Gravité:** 🟠 MAJEURE —Structure confuse, incompréhensible

**Location:** [preamble.tex](preamble.tex) lignes 40-70 et 160-180 (deux sections fancyhdr)

**Problème:**
- Première définition fancyhdr (lignes 40-70):
  ```latex
  % ← Première tentative
  \fancyhead[L]{\sffamily\small Mathématiques Appliquées}
  \fancyfoot[L]{\sffamily\small BTS FED A -- \leftmark}
  \fancyfoot[R]{\sffamily\small Page \thepage\ / \pageref{lastpage:\thechapter}}
  ```

- Deuxième définition fancyhdr (lignes 160-180):
  ```latex
  % ← Deuxième tentative (écrase la première!)
  \fancyhead[LE,RO]{\small\textcolor{btsprimary}{\textit{BTS FED — Option GCF}}}
  \fancyhead[RE,LO]{\small\textcolor{btsprimary!70!black}{\nouppercase{\leftmark}}}
  \fancyfoot[C]{\small\textcolor{btsprimary!60!black}{--- \thepage\ ---}}
  ```

**Résultat:**
- La première définition est écrasée par la deuxième
- La deuxième utilise des couleurs invalides (`btsprimary` non défini!)
- Confusing: l'intention est-elle vraiment d'avoir deux en-tête systems? ❌

---

## 🟠 INCOHÉRENCES MAJEURES

### 3. **Exercices sans structure graphique (contrairement à la charte)**

**Gravité:** 🟠 MAJEURE — Pas de cohésion visuelle

**Location:** [exercices/00-exercices.tex](exercices/00-exercices.tex) (fichier en entier, 283 lignes)

**Problème:**
Le preamble définit 7 environnements tcolorbox de haute qualité:
- ✓ `\begin{definition}` (blue avec barre gauche)
- ✓ `\begin{propriete}` (orange avec border)
- ✓ `\begin{exemple}` (green avec traits pointillés)
- ✓ `\begin{erreur}` (red warning)
- ✓ **`\begin{exercice}` (style dark themed)**
- ✓ `\begin{methode}` (orange)
- ✓ `\begin{attention}` (red warning)

**Mais dans exercices/00-exercices.tex:**
```latex
% ← Actuellement: structure MINIMALISTE
\subsection*{Thème A — Vérification d'homogénéité (6 exercices)}
\subsubsection*{A1}  Perte de charge : $\Delta P = ...$
\subsubsection*{A2}  Bilan thermique : $\dot{Q} = ...$
% ... pas de boîtes colorées
```

**Attendu (selon la charte):**
```latex
% ← Devrait ressembler à:
\begin{exercice}[A1]
  Perte de charge : $\Delta P = ...$
\end{exercice}

\begin{exercice}[A2]
  Bilan thermique : $\dot{Q} = ...$
\end{exercice}
```

**Impact visuel:**
- Les chapitres théoriques (01, 11) utilisent les boîtes ✓
- Les exercices: simples titres sans mise en évidence ❌
- Rupture de style très noticeable (perte de la guidance visuelle)

---

### 4. **Pages de titre : Cohérence PARTIELLE (bonne mais l'une ou l'autre...)**

**Gravité:** 🟡 MINEURE — Travail correct, mais pattern flou

**Location:** [main.tex](main.tex) et [livret-exercices.tex](livret-exercices.tex) , lignes 8-50

**Analyse:**

✓ **main.tex** (cours):
```latex
\begin{tcolorbox}[..., colback=FedBlue, ...]  % Bande bleu à gauche
\end{tcolorbox}
\node[rotate=90, anchor=west, white] at ... {\sffamily\Huge\bfseries MATHÉMATIQUES}
% ← Correct, utilise FedBlue
```

✓ **livret-exercices.tex** (exercices):
```latex
\begin{tcolorbox}[..., colback=FedOrange, ...]  % Bande orange à gauche
\end{tcolorbox}
\node[rotate=90, anchor=west, white] at ... {\sffamily\Huge\bfseries EXERCICES}
% ← Correct, utilise FedOrange
```

**Bon point:** Les pages de titre utilisent correctement la palette FED  
**Mauvais point:** Aucun lien visuel/sémantique explicitant pourquoi main.tex = blue et livret = orange

---

### 5. **Environnement `\methode` avec paramètre non-standard**

**Gravité:** 🟡 MINEURE — Risque de confusion d'usage

**Location:** [preamble.tex](preamble.tex) lignes 120-125 vs [chapitres/11-etudes-de-cas.tex](chapitres/11-etudes-de-cas.tex) lignes 15-45

**Problème:**

Définition dans preamble:
```latex
\newtcolorbox{methode}[1][]{
  % [1][] = optionnel (description générale)
  title={MÉTHODE~: #1}, 
  ...
}
```

Usage dans 11-etudes-de-cas.tex:
```latex
\begin{methode}[title={Étapes du dimensionnement CVC}]  % ← PARAMÈTRE NOMMÉ!
  ...
\end{methode}
```

**Problème:**
- La définition tcolorbox attend **`[description]`** pas **`[title=...]`**
- La syntaxe utilisée dans le chapitre 11 est celle de **tcolorbox** (paramètre du boîte directement)
- Mais la définition ne passela par cette option aucun moyen!
- **Cela va probablement échouer à la compile ou ignorer le `title=`**

Comparaison avec usage correct dans le même chapitre:
```latex
\begin{definition}[title={Note de calcul}]  % ← Pour definition, ça marche
  ...
\end{definition}
```

---

## 🟢 POINTS POSITIFS (appliqués correctement)

### ✓ Utilisation des boîtes de couleur dans les chapitres

**Location:** [chapitres/01-bases-thermiques.tex](chapitres/01-bases-thermiques.tex) et [chapitres/11-etudes-de-cas.tex](chapitres/11-etudes-de-cas.tex)

**Exemples:**
```latex
\begin{definition}
  \textbf{Température} (\(T\)) : grandeur intensive...
\end{definition}
```
✓ Utilisé correctement dans chapitres 00, 01, 11

```latex
\begin{methode}[title={Étapes du dimensionnement CVC}]
  \begin{enumerate}
    \item Collecte des données...
  \end{enumerate}
\end{methode}
```
✓ Identifiés dans chapitre 11 (peut-être avec une syntaxe discutable)

```latex
\begin{attention}
  En pratique, le pincement thermique fixe...
\end{attention}
```
✓ Utilisé correcment dans chapitre 11

---

### ✓ Cohérence des couleurs (quand elles s'exécutent)

- `FedBlue` : titres principaux, bandes décoratives, cadres de principaux
- `FedOrange` : accents, bordures, mise en évidence d'étapes
- `FedRed` : avertissements, erreurs
- `FedGreen` : exemples
- Palette **bien pensée et esthétique** ✓

---

## 📋 TABLEAU COMPARATIF — Utilisation de la Charte

| Fichier | Importe Preamble? | Utilise Couleurs FED? | Utilise Boîtes? | Statut |
|---------|:-:|:-:|:-:|---------|
| **main.tex** | ✓ | ✓ FedBlue, Orange | Partiellement (page titre seulement) | 🟡 Partiel |
| **livret-exercices.tex** | ✓ | ✓ FedOrange, Blue | Partiellement (page titre seulement) | 🟡 Partiel |
| **00-analyse-dimensionnelle.tex** | Via `\chapter` | Via preamble | ✓ (definition, exemple) | 🟢 Bon |
| **01-bases-thermiques.tex** | Via `\chapter` | Via preamble | ✓✓ (definition, convection, etc.) | 🟢 Excellent |
| **11-etudes-de-cas.tex** | Via `\chapter` | Via preamble | ✓✓ (methode, definition, attention) | 🟢 Excellent |
| **00-exercices.tex** | Via preamble | ✗ Non utilisées | ✗ Aucune | 🔴 Critique |
| **preamble.tex** | N/A | Partiellement (début ✓, fin ✗) | ✓ (définition) mais rupture | 🔴 Critique |

---

## 🛠️ RECOMMANDATIONS PAR PRIORITÉ

### PRIORITÉ 1 (Critique — réparer avant compilation)

**1.1) Définir les alias de couleurs manquants**
```latex
% Ajouter après ligne 35 dans preamble.tex:

% Alias pour compatibilité avec styles titre/env
\definecolor{btsprimary}{RGB}{0, 92, 122}      % ← FedBlue
\definecolor{btsaccent}{RGB}{217, 90, 64}      % ← FedOrange
\definecolor{btsrule}{RGB}{0, 92, 122}         % ← FedBlue

% Mode alternatif (plus logique):
% Remplacer TOUTES occurrences de btsprimary/btsaccent/btsrule par FedBlue/FedOrange
```

**1.2) Nettoyer la duplication fancyhdr**
- Garder SOLA la section lignes 160-170 (celle avec \textcolor)
- Supprimer les lignes 40-70 (devenues obsolètes)
- Ou fusionner intelligemment

---

### PRIORITÉ 2 (Majeure — compléter la charte)

**2.1) Restructurer les exercices avec boîtes**

Remplacer la structure actuelle de [exercices/00-exercices.tex](exercices/00-exercices.tex):
```latex
% ❌ ACTUELLEMENT:
\subsubsection*{A1}  Perte de charge : ...
```

Par:
```latex
% ✓ À FAIRE:
\begin{exercice}[A1 — Perte de charge]
  $\Delta P = \lambda \dfrac{\ell}{d} \dfrac{\rho v^2}{2}$. Vérifier.
\end{exercice}

% ou, niveau par niveau:
\subsection*{Thème A — Vérification d'homogénéité}
\begin{exercice}
  (A1) Perte de charge : ...
\end{exercice}
\begin{exercice}
  (A2) Bilan thermique : ...
\end{exercice}
```

**2.2) Corriger la syntaxe `\methode`**

Dans preamble.tex lignes 122-126:
```latex
% ❌ ACTUELLEMENT:
\newtcolorbox{methode}[1][]{
  enhanced, colback=FedOrange!5, colframe=FedOrange, 
  fonttitle=\bfseries\sffamily,
  coltitle=FedOrange, title={MÉTHODE~: #1}, 
  ...
}

% ✓ Option A — Accepter les paramètres nommés:
\newtcolorbox{methode}[1][]{
  enhanced, colback=FedOrange!5, colframe=FedOrange, 
  fonttitle=\bfseries\sffamily, coltitle=FedOrange,
  title={MÉTHODE\ifx#1\empty\else~: ~#1\fi}, 
  boxrule=1pt, arc=2pt, width=\textwidth, nobeforeafter
}

% ✓ Option B — Créer un nouveau env avec param nommé:
\tcbset{
  methode/.style={
    enhanced, colback=FedOrange!5, colframe=FedOrange, 
    fonttitle=\bfseries\sffamily, coltitle=FedOrange,
    title={MÉTHODE},...
  }
}
```

---

### PRIORITÉ 3 (Mineure — améliorer la clarté)

**3.1) Ajouter des commentaires explicatifs dans preamble.tex**
```latex
% Clarifier: "Cette section configure les BOÎTES de couleur (en haut du document)"
% vs. "Cette section configure la MISE EN PAGE (headers/footers, table of contents)"
```

**3.2) Documenter le pattern de couleurs par document**
```latex
% main.tex:
%   - Page titre: FedBlue (cours/théorie)
%   - Références: [section] → FedBlue

% livret-exercices.tex:
%   - Page titre: FedOrange (exercices/application)
%   - Références: [exercice] → FedExercice ou Orange
```

**3.3) Standardiser l'usage des boîtes**
- Créer un guide de style: quand utiliser `definition` vs `exemple` vs `propriete`
- Documenter la structure cible pourfutur du livret

---

## 📊 Résumé Exécutif

| Critère | État | Note |
|---------|------|------|
| **Palette de couleurs** | Définie mais partiellement utilisée | 6/10 |
| **Boîtes tcolorbox** | Bien définies, usage inconsistant | 5/10 |
| **Structuration des chapitres** | Bon dans théorie, absent dans exercices | 4/10 |
| **Cohérence globale** | Pages titre OK, reste problématique | 3/10 |
| **Compilabilité** | ❌ Couleurs manquantes bloquent compile | 0/10 |

**VERDICT:** 🔴  
Charte graphique **partiellement implémentée** mais **inutilisable en l'état**.  
Blocages critiques à CORRECTION: alias `bts*`, duplication fancyhdr, exercices restructuration.

---

**Généré par analyse automatisée — 7 avril 2026**
