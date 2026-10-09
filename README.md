# 💘 Projet Speed Dating : qu'est-ce qui donne envie de se revoir ?

Projet d'analyse de données réalisé pour la certification Jedha Fullstack (Bloc 2, analyse exploratoire).

## En 30 secondes

Tinder voit baisser ses mises en relation. À partir d'une expérience de speed dating (8378 rendez-vous
de 4 minutes), j'ai cherché ce qui pousse deux personnes à dire « Oui, je veux te revoir ».
Ce qui compte le plus : **l'attirance**, **l'humour** et surtout les **intérêts communs** (66,8 % de « Oui »
quand ils sont forts, contre 31,6 % quand ils sont faibles). Avoir la même origine change très peu le résultat
(45,0 % contre 42,2 %).

## 1. Le problème (côté business)

Tinder constate une **baisse du nombre de mises en relation**. L'équipe marketing veut comprendre
**ce qui donne envie à deux personnes de se revoir**, pour améliorer l'application.

Pour cela, Tinder a organisé une expérience de **speed dating** (2002-2004) : chaque participant
a eu des rendez-vous de 4 minutes avec d'autres personnes. À la fin de chaque rendez-vous, il a
répondu **Oui ou Non** à la question « Veux-tu revoir cette personne ? » et l'a **notée sur 6 critères** :
attirance, sincérité, intelligence, humour, ambition, intérêts communs.

## 2. Les données

- **8378 rencontres** (une ligne = un rendez-vous de 4 minutes) et **195 colonnes**.
- Fichier fourni par Jedha :
  [Speed Dating Data.csv](https://full-stack-assets.s3.eu-west-3.amazonaws.com/M03-EDA/Speed+Dating+Data.csv)
  (description des colonnes : [Data Key](https://full-stack-assets.s3.eu-west-3.amazonaws.com/M03-EDA/Speed+Dating+Data+Key.doc)).
- ⚠️ **Le fichier de données n'est pas dans ce dépôt GitHub** (je ne publie pas les données).
  Pour relancer le projet, télécharge-le, renomme-le `speed_dating.csv` et mets-le dans le dossier `data/`.
  Il est lu avec l'encodage `latin-1`.

## 3. Ce que contient le notebook

Le notebook `notebooks/01-Speed_Dating.ipynb` suit ces étapes. Chaque étape a un titre, une
explication du « pourquoi », le code, puis « ce que je vois / ce que ça veut dire ».

| Étape | Question | Ce que je fais |
|---|---|---|
| 0 | Quelles données j'ai ? | Je charge le fichier et je regarde sa taille |
| 1 | Où sont les cases vides ? | Je compte les cases vides et je compare avant/après suppression |
| 2 | Comment je nettoie ? | Je garde 10 colonnes utiles sur 195 et je supprime les lignes incomplètes |
| 3 | Les notes et âges sont-ils réalistes ? | Je vérifie que les notes sont entre 0 et 10 et que les âges sont plausibles |
| 4 | Quel critère est le plus lié au « Oui » ? | Corrélation de Pearson, graphique en barres |
| 5 | L'attirance compte-t-elle ? | Note d'attirance moyenne quand c'est Oui et quand c'est Non |
| 6 | Qu'est-ce qui fait dire « Oui » ? | Écart de note entre Oui et Non pour chaque critère |
| 7 | Premier ou dernier rendez-vous ? | Taux de « Oui » selon la position dans la soirée |
| 8 | Intérêts communs ou même origine ? | Taux de « Oui » selon les intérêts communs et l'origine |
| 9 | Calcul en parallèle | Même calcul avec PySpark, comparé à Pandas |
| 10 | Que conseiller à Tinder ? | Conclusion et 3 recommandations |

## 4. Résultats principaux

**Nettoyage :** sur 8378 rencontres, 7031 sont complètes (**16,1 % de lignes supprimées**).
La colonne la plus incomplète est celle des intérêts communs (12,7 % de cases vides).
Les 6 notes sont toutes entre 0 et 10, et les âges vont de 18 à 55 ans (médiane : 26 ans).

**Ce qui est lié au « Oui »** (corrélation : plus c'est proche de 1, plus le lien est fort) :

| Critère | Lien avec le « Oui » |
|---|---|
| Attirance | 0,49 |
| Humour | 0,41 |
| Intérêts communs | 0,40 |
| Sincérité | 0,21 |
| Intelligence | 0,21 |
| Ambition | 0,18 |

**Intérêts communs ou même origine ?**
- Intérêts communs forts (note ≥ 7) : **66,8 %** de « Oui » ; faibles : **31,6 %**. Écart : 35,2 points.
- Même origine : 45,0 % de « Oui » ; origine différente : 42,2 %. Écart : 2,8 points.
- Les intérêts communs comptent donc beaucoup plus que l'origine commune.

**Position dans la soirée :** le taux de « Oui » est de **49,9 %** au premier rendez-vous, **41,2 %** pour ceux du milieu et
**44,5 %** au dernier. Être premier donne donc un petit avantage (8,7 points de plus que le milieu, 5,4 de plus que le dernier).
Je n'ai pas vérifié si cet écart pourrait être dû au hasard.

**Hommes et femmes (calcul Spark, vérifié avec Pandas) :** les hommes disent « Oui » dans **47,4 %** des
rencontres, les femmes dans **36,5 %**.

## 5. Recommandations pour Tinder

1. **Mettre en avant les intérêts communs** entre deux profils : c'est ce qui fait le plus bouger le taux de « Oui ».
2. **Soigner la présentation visuelle des profils** (photos) : l'attirance est le critère le plus lié au « Oui ».
3. **Laisser de la place à l'humour et à la personnalité** dans les biographies : l'humour arrive juste derrière.

## 6. Limites (ce qu'il faut savoir)

- Ce sont des **liens** (corrélations), pas des **causes** : « les deux vont ensemble » ne prouve pas que l'un provoque l'autre.
- Les données viennent d'une **expérience de 2002-2004**, pas d'utilisateurs actuels de Tinder.
- J'ai supprimé les lignes incomplètes (16,1 %). Je n'ai pas poussé plus loin la vérification que l'échantillon reste équilibré
  (c'est l'objet de l'étape 1 du notebook).
- Les notes sont données **après** la rencontre, elles peuvent être influencées par l'envie de dire « Oui ».
- Le seuil « intérêts communs forts » (note ≥ 7) est un **choix de ma part**.
- Pour la position dans la soirée, je n'ai pas comparé le nombre de rencontres de chaque groupe.
- **Spark tourne sur mon ordinateur** (mode « local »), pas sur plusieurs machines. Avec si peu de lignes,
  Pandas est aussi rapide : je montre la méthode, qui fonctionnerait aussi avec des millions de lignes.

## 7. Relancer le projet

Il faut Python 3 et, pour la partie Spark, **Java 17 ou plus récent**.

1. Récupérer le projet :
```
   git clone git@github.com:Carelle777/projet_01_speed_dating.git
   cd projet_01_speed_dating
```
2. Créer un environnement et installer les outils :
```
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
```
3. Mettre le fichier de données dans `data/speed_dating.csv` (voir section 2).
4. Ouvrir `notebooks/01-Speed_Dating.ipynb` (VS Code ou Jupyter) et lancer toutes les cellules (*Run All*).

**Java pour Spark (Mac) :** `brew install openjdk@17`. Dans le notebook, le chemin de Java est écrit pour un Mac avec
Homebrew (`/opt/homebrew/opt/openjdk@17/...`). Sur un autre ordinateur, il faut adapter cette ligne. Sans Java 17,
l'étape 9 échoue avec l'erreur `JAVA_GATEWAY_EXITED`, mais le reste du notebook fonctionne.

## 8. Structure du projet

```
projet_01_speed_dating/
├── notebooks/
│   └── 01-Speed_Dating.ipynb   ← le notebook d'analyse
├── data/                       ← les données (non publiées, voir section 2)
├── requirements.txt            ← les outils Python à installer
├── .gitignore                  ← fichiers à ne pas envoyer sur GitHub
└── README.md                   ← ce fichier
```

## 9. Lexique (mots simples)

- **EDA** (analyse exploratoire) : regarder les données avec des chiffres et des graphiques pour comprendre ce qu'elles disent.
- **Case vide (NaN)** : une information manquante dans le tableau.
- **Corrélation de Pearson** : un chiffre entre -1 et 1 qui dit si deux choses évoluent ensemble. Proche de 1 : elles montent ensemble. Proche de 0 : pas de lien.
- **Valeur atypique** : une valeur très différente des autres (par exemple un âge de 55 ans quand presque tout le monde a entre 24 et 28 ans).
- **Pandas** : l'outil Python pour manipuler des tableaux de données.
- **Plotly** : l'outil Python pour faire des graphiques.
- **Spark (PySpark)** : un outil qui coupe les données en morceaux et les traite en même temps. Utile avec de très gros fichiers.
- **Mode « local »** : Spark tourne sur un seul ordinateur, avec plusieurs cœurs de processeur.