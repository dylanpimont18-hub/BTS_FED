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
