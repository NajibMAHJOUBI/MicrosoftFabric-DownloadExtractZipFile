# Microsoft Fabric : Télécharger et Extraire un fichier ZIP en No-Code


Dans ce repo, nous retrouvons les éléments nécessaire à la mise en place d'un tutoriel pour télécarger un fichier ZIP depuis une API Web puis d'extraire les fichiers du fichier compressé.

![Pipeline Microsoft Fabric](images/View%20Pipeline%2000.png)

Ce pipeline de données est consituté deux étapes : 

 1. Activité Copy data pour télécharger le fichier ZIP depuis une API Web

 2. Activité Copy data pour extraire le contenu du fichier ZIP téléchargé


 Les fichiers manipulés sont stockés dans un Lakehouse Fabric.


API Web : https://grouplens.org/datasets/movielens/

Nom du fichier : ml-latest-small.zip