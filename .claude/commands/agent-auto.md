# Agent automatisé BTS FED GCF — Exécution toutes les 5h

Tu es un agent d'amélioration continue du cours BTS FED option GCF.
Tu travailles sur le dépôt `c:\Users\Dylan\Desktop\Creation_site\BTS_FED`.
**Ce prompt est auto-suffisant** — tu n'as aucun contexte de conversation précédent.

---

## Étape 1 — Synchroniser le dépôt

```bash
cd "c:\Users\Dylan\Desktop\Creation_site\BTS_FED"
git pull origin main
```

Si des conflits de merge apparaissent, abandonne le pull et arrête-toi :
signale l'erreur dans un commit message `fix: conflit git — intervention manuelle requise`.

---

## Étape 2 — Lire l'état du cours

Lis **uniquement** `cours/state.md`.

Dans la section **"Prochain focus — Tâches pour l'agent automatisé"**, repère :
1. Les 2 premières lignes avec `Statut = TODO` et `Priorité = HAUTE`
2. Si moins de 2 lignes HAUTE, complète avec MOYENNE
3. **Règle de non-conflit :** les 2 tâches choisies doivent cibler des fichiers différents

**Note les 2 tâches choisies :** ID, fichier cible, description.

Mets immédiatement à jour `cours/state.md` : change le statut de ces 2 tâches de `TODO` → `EN_COURS`.

---

## Étape 3 — Lancer 2 sous-agents en parallèle

Lance exactement **2 sous-agents background** (jamais plus), un par tâche.

Chaque sous-agent reçoit un prompt autonome contenant :
- Le chemin absolu du fichier à modifier
- La description exacte de la tâche (copie depuis state.md)
- Le contexte technique nécessaire (extrait ci-dessous selon le type de tâche)

### Contexte à transmettre selon le type de tâche

**Si la tâche concerne un `.tex` de chapitre :**
```
Fichier : [chemin absolu]
Preamble disponible : cours/preamble.tex
Couleurs : FedBlue(0,92,122), FedOrange(217,90,64), FedGreen(74,124,89), FedRed(192,57,43)
Boîtes tcolorbox : definition, methode, attention, exemple, exercice, erreur
TikZ librairies : shapes.geometric, arrows.meta, positioning
Ne modifie PAS state.md, main.tex, preamble.tex.
Langue : français intégral.
```

**Si la tâche concerne `livret-exercices.tex` (T01) :**
```
Fichier : cours/livret-exercices.tex
Ajouter les \input manquants pour les chapitres 01-07 dans l'ordre, avant le chapitre 08.
Les fichiers existent déjà dans cours/exercices/01-exercices.tex à 07-exercices.tex.
Ne modifie PAS d'autres fichiers.
```

**Si la tâche concerne un profil étudiant `.md` (T02/T03/T04) :**
```
Fichier : cours/[etudiant-xxx.md]
Rédige un profil pédagogique complet en markdown (300 mots minimum) :
- Profil type de l'étudiant (comportement, lacunes ou forces, autonomie)
- Adaptations pédagogiques recommandées dans le cours BTS FED GCF
- Exercices ou chapitres prioritaires à lui proposer
- Stratégie d'évaluation adaptée
Langue : français intégral.
```

**Si la tâche concerne `preamble.tex` (T17 — fichemémo) :**
```
Fichier : cours/preamble.tex
Ajouter APRÈS la définition de \begin{methode} l'environnement suivant :
\newtcolorbox{fichememo}[1][]{
    enhanced, colback=FedBlue!3, colframe=FedBlue!50,
    fonttitle=\bfseries\sffamily, coltitle=FedBlue,
    title={FICHE MÉMO — #1}, boxrule=0.8pt, arc=2pt,
    width=\textwidth, nobeforeafter
}
Ne modifie rien d'autre.
```

---

## Étape 4 — Attendre les résultats

Attends la complétion des 2 sous-agents.

Pour chaque sous-agent :
- Si succès : note le résumé des modifications
- Si échec : note l'erreur, ne marque pas la tâche comme FAIT

---

## Étape 5 — Mettre à jour state.md

Dans `cours/state.md` :
- Tâches réussies : `EN_COURS` → `FAIT`
- Tâches échouées : `EN_COURS` → `TODO` (réinitialisation)
- Mets à jour **Dernier run** avec la date du jour et l'action effectuée

---

## Étape 6 — Commiter et pousser

```bash
cd "c:\Users\Dylan\Desktop\Creation_site\BTS_FED"
git add cours/
git commit -m "agent(auto): [tâche1-ID] + [tâche2-ID] — $(date +%Y-%m-%d)"
git push origin main
```

---

## Règles absolues

- **Maximum 2 sous-agents simultanément** (quota Claude)
- **Jamais 2 tâches sur le même fichier** dans le même run
- **Ne pas modifier** `main.tex`, `preamble.tex`, `state.md` dans les sous-agents (seulement dans l'orchestrateur)
- **Si aucune tâche TODO disponible** : log "Aucune tâche disponible" et arrête sans commiter
- **Langue de tous les fichiers .tex** : français intégral, terminologie professionnelle GCF
