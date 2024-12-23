# Accidentologie - Étude des circonstances des accidents de la route en France de 2005 à 2022

Emmanuel Gautier - Erika Méronville

Vers la page streamlit :
https://accidentologie-fkzj2g9g5tm5go8rrd6xpn.streamlit.app/

------------
# Présentation

Ce dépôt réunit les éléments de notre projet de machine learning que nous avons réalisé lors de notre formation dispensée par 
[DataScientest](https://datascientest.com/).

Plus précisément, ce projet porte sur le thème des accidents de la route en France au cours de la période de 2005 à 2022. Les données ainsi que 
leur description sont disponibles sur le site www.data.gouv.fr.

Ces données concernent 72 dataframes au total, soit 1 dataframe par année et par rubrique.
Un changement de codage de la gravité entre 2018 et 2019 nous contraint de ne retenir
que les données de 2019 à 2022, soit les quatre dernières années.

Voici les rubriques concernées par l'étude :

 — caracteristiques : qui prend en compte les circonstances générales de l’accident.

 — lieux : qui décrit l’endroit de l’accident.

 — vehicules : qui énonce les véhicules impliqués dans l’accident.

 — usagers : qui relate les usagers impliqués dans l’accident.

L’objectif principal consiste à explorer, préparer et modéliser le jeu de données complet dans le but de prédire la gravité des accidents routiers 
en fonction des circonstances qui les entourent.

------------
# Architecture

## notebooks 

*11_Exploration.ipynb* : 
 - examen de la structure et des types de variables pour chaque fichier, 
 - étude de la distribution, des valeurs manquantes, des outliers et de l’évolution temporelle
 - repérage des incohérences, des changements de codification et des valeurs aberrantes

*21_preprocessing_1.ipynb* :
 - restructuration des dataframes, harmonisation des types de données et fusion des données des différentes rubriques
 - création de nouvelles variables et élimination de certaines variables jugées non pertinentes

*22_preprocessing_2.ipynb* :
 - catégorisation et dichotomisation des variables pertinentes
 - traitement des valeurs manquantes et aberrantes
 - équilibrage des classes pour la variable cible et réduction de dimensionnalité par PCA (100 composantes)

*31_Modelisation_LR.ipynb* :
 - modèle de référence basé sur le premier preprocessing : régression logistique
 - très faible performance (accuracy de 59%) et limitations en termes de relations non linéaires

*32_modelisation_ML.ipynb* :
- multiples modèles de classification sur le deuxième preprocessing
- comparaison entre plusieurs modèles :
    - SVC (Support Vector Classification)
    - Régression logistique
    - Gradient Boosting
    - Arbres de décision
    - Random Forest, etc.
- meilleurs résultats par rapport au premier preprocessing :
    - SVM : score AUC-ROC de 0.781 et recall pour vrais positifs de 0.827
    - Gradient Boosting : bonne performance avec temps de calcul raisonnable

*33_modelisation_3.ipynb* :
 - modèle Deep Learning (réseau de neurones) avec architecture optimisée
 - bonne performance (score AUC-ROC de 0.857 et recall pour vrais positifs de 0.81)

## models
Contient les principaux modèles entrainés. Les modèles trop volumineux n'y sont pas.

## references
 - desc_fic_raw.json : informations sur les fichiers sources permettant leur chargement en DataFrames.
 - desc_vars.json : dictionnaire des variables et modalités avec types de variables et libellés explicites.

## reports
Contient le rapport final au format pdf

------------
# Meilleurs résultats des modèles entrainés
| N° Entrainement | Nom du Modèle | AUC-ROC | Recall (Vrais Positifs) |
|-----------------|---------------|---------|-------------------------|
| 1 | Régression Logistique | 0.59 | - |
| 2 | SVM | 0.781 | 0.827 |
| 3 | Deep Learning | 0.857 | 0.81 |

------------
# Exécution des notebooks
1. Télécharger les données des accidents de la route en France sur le site [www.data.gouv.fr](https://www.data.gouv.fr/fr/)
2. Créer les dossiers suivants dans votre environnement Jupyter Notebook :
    - `data/raw/` : pour les fichiers CSV téléchargés
    - `data/processed/` : pour les fichiers générés lors du preprocessing
3. Installer les dépendances nécessaires : `pip install -r requirements.txt`
4. Copier les notebooks du repository GitHub dans votre environnement Jupyter Notebook
5. Exécuter les notebooks dans l'ordre indiqué

 Nota bene : Les fichiers de données étant volumineux, ils ne sont pas inclus dans ce repository.
 Veillez à bien les télécharger et les placer dans le dossier `data/raw/` avant d'exécuter les notebooks.
