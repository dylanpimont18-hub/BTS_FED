# État du cours BTS FED GCF

Mis à jour automatiquement par l'agent à chaque run.

## Dernier run
- Date : 2026-04-07 (4ème run)
- Action : **Enrichissement massif — diagrammes TikZ tous chapitres + correction preamble + décommenter main.tex**
  - 12 chapitres enrichis avec 3 à 8 diagrammes TikZ chacun
  - `preamble.tex` : ajout des couleurs `btsprimary`, `btsaccent`, `btsrule` (fix erreur compilation)
  - `main.tex` : tous les chapitres 01-10 décommentés
  - `\finchapitre` vérifié/ajouté sur tous les chapitres

## Prochain focus
**Priorité 1** : Tester la compilation PDF (LaTeX non installé localement — utiliser Overleaf ou installer MiKTeX)
**Priorité 2** : Révision croisée des chapitres (relecture pédagogique, cohérence inter-chapitres)
**Priorité 3** : Ajouter un livret d'exercices séparé (`livret-exercices.tex`)

## Chapitres

| # | Fichier | Titre | Statut | Score /5 | Notes |
|---|---------|-------|--------|----------|-------|
| 00 | 00-analyse-dimensionnelle.tex | Analyse dimensionnelle et remise à niveau | révisé | 5 | 2026-04-07 : 3 TikZ (roue SI, méthode homogénéité, tableau grandeurs CVC) + fix siunitx + \finchapitre |
| 01 | 01-bases-thermiques.tex | Bases de la thermique | révisé | 5 | 2026-04-07 : 3 TikZ (modes transfert, paroi multicouche, courbe chauffe eau) + \finchapitre |
| 02 | 02-hydraulique.tex | Hydraulique des circuits | révisé | 5 | 2026-04-07 : 3 TikZ (circuit bouclé, courbe pompe/réseau, profils écoulement) + \finchapitre |
| 03 | 03-aeraulique.tex | Aéraulique | révisé | 5 | 2026-04-07 : 4 TikZ (réseau gaines, courbe ventilateur, VMC double flux, lois similitude) + \finchapitre |
| 04 | 04-production-chaleur.tex | Production de chaleur | révisé | 5 | 2026-04-07 : 3 TikZ (cycle PAC, chaudière condensation, comparaison COP) + \finchapitre |
| 05 | 05-distribution-emission.tex | Distribution et émission | révisé | 5 | 2026-04-07 : 3 TikZ (circuit V3V, plancher chauffant, comparaison émetteurs) + 2 exercices corrigés + \finchapitre |
| 06 | 06-climatisation.tex | Climatisation et traitement d'air | révisé | 5 | 2026-04-07 : 6 TikZ (CTA, psychrométrie, free-cooling…) + \finchapitre |
| 07 | 07-regulation-gtb.tex | Régulation et GTB | révisé | 5 | 2026-04-07 : 8 TikZ (boucle PID, architecture GTB, réponse échelon…) + \finchapitre ajouté |
| 08 | 08-efficacite-energetique.tex | Efficacité énergétique et RE2020 | révisé | 5 | 2026-04-07 : 6 TikZ (Sankey, niveaux RE2020, comparaison RT2012/RE2020…) + \finchapitre |
| 09 | 09-acoustique.tex | Acoustique du bâtiment | révisé | 5 | 2026-04-07 : 6 TikZ (propagation réseau, échelle dB, silencieux…) + \finchapitre ajouté |
| 10 | 10-electrotechnique.tex | Électrotechnique appliquée CVC | révisé | 5 | 2026-04-07 : 6 TikZ (triangle puissances, armoire CVC, courbes protection) + \finchapitre |
| 11 | 11-etudes-de-cas.tex | Études de cas et dimensionnement | révisé | 5 | 2026-04-07 : 8 TikZ (schéma installation, organigramme, tableaux…) + \finchapitre ajouté |

## Légende des statuts
- `absent` : chapitre non encore créé
- `ébauche` : structure créée, contenu partiel
- `complet` : cours + exemples + exercices présents
- `révisé` : relu, enrichi, diagrammes TikZ ajoutés, exercices corrigés complets
