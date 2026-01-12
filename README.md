# Microsoft Fabric : Télécharger et Extraire un fichier ZIP en No-Code


Dans ce tutoriel, nous allons présenter comme télécharger des fichiers ZIP depuis une URL puis comment extraire le contenu du fichier téléchargé dans Lakehouse. Pour cela, nous allons privilégier une approche No-Code dans Microsoft Fabric.


## Prérequis

 - Un abonnement Microsoft Fabric activé
 - Un workspace avec une capacité.
 
## Scénario

Pour illustrer ce tutoriel, nous proposons de mettre en place la scénario suivant :

 1. Télécharger un fichier .zip disponible en libre service sur le site de MovieLens
 2. Extraire les fichiers .csv du fichier .zip télécharger

L'ensemble des données seront placées dans un Lakehouse et les tâches seront mises en place dans un Pipeline de données.

## Créer un Lakehouse

Nous allons commencer par créer un Lakehouse qui servira à héberger les données de ce projet. Depuis la page d'accueil de l'interface Microsoft Fabric, suivre les étapes suivantes :

1. Cliquer sur le bouton **+ New item**
2. Depuis le champ de recherche, taper le mot : lakehouse
3. Cliquer sur l'item **Lakehouse**

![](images/Create%20Lakehouse%2000.png)


Cela va ouvrir une fenêtre permettant de nommer ce Lakehouse en suivant les étapes suivantes :

1. Dans le champ **Name**, entrer un nom pour ce nouveau Lakehouse. Dans notre exemple, nous le nommons Demo_LK.
2. Dans le champ **Location**, choisir le Lakehouse à utiliser. Dans cet exemple, notre Lakehouse se nomme Tutoriel Download Extract ZIP.
3. Cliquer sur le bouton **Create**

![](images/Create%20Lakehouse%2001.png)


## Créer un Pipeline

Pour orchestrer le scénario proposé, nous allons mettre en place un Pipeline de données dans Microsoft Fabric. Commençons par le créer en suivant les étapes suivantes :

1. Depuis l'interface du Workspace utilisé, cliquer sur le bouton **+ New item**
2. Dans le volet qui apparaît à droite et le champ de recherche, entrer le mot pipeline
3. Cliquer sur l'item **Pipeline** dans le volet **Get Data**

![](images/Create%20Pipeline%2000.png)


Dans la fenêtre **New pipeline**, nous allons pouvoir nommer ce Pipeline en suivant les étapes suivantes :

1. Dans le champ **Name**, entrer un nom pour ce Pipeline. Dans notre exemple, nous allons le nommer *Download Extract ZIP File*
2. Cliquer sur le bouton **Create**

![](images/Create%20Pipeline%2001.png)

A présent que nous avons créé ce pipeline, nous allons mettre en place les différentes étapes utiles à notre projet.


## Télécharger un fichier ZIP

Afin de télécharger un fichier ZIP avec une approche No-Code, nous vous proposons de suivre les étapes suivantes :

- **Etape 1 : Ajouter une activité Copy data**

  1. Depuis l'interface de notre Pipeline, cliquer sur l'option **Copy data**
  
  2. Puis cliquer sur **Add to canvas**

![](images/Copy%20Data%20HTTP%2000.png)

 - **Etape 2 : Paramètre Général de l'activité Copy data**

    1. Sélectionner l’icône de l'activité **Copy data** depuis la représentation schématique de workflow

    2. Dans le volet du bas, cliquer sur le menu **Général**

    3. Dans le champ **Name**, entrer un nom de votre choix pour nommer l'activité. Dans notre exemple, nous le nommons *Download ZIP File*

![](images/Copy%20Data%20HTTP%2001.png)

- **Etape 3 : Paramètre Source de l'activité Copy data**

    1. Cliquer sur le menu **Source**
    
    2. Dans le champ **Connexion**, sélectionner l'option Browse all

![](images/Copy%20Data%20HTTP%2002.png)

Cela va ouvrir la fenêtre **Get data** qui va permettre de poursuivre la définition de la source de données en suivant les étapes suivantes :

1. Dans le champ de recherche **Choose a data source to get started**, taper le mot http,
    
2. Choisir l'option **Http** dans le champ **New sources**

![](images/Copy%20Data%20HTTP%2003.png)

Après l'ouverture de la fenêtre **Connect data source**, nous allons pouvoir renseigner l'URL de la source en suivant les étapes suivantes:

1. Dans le champ **Connection settings**, entrer l'URL du fichier ZIP à télécharger. Dans notre exemple, nous allons utiliser un fichier ZIP mis à disposition sur le site [MovieLens](https://files.grouplens.org/datasets/movielens/ml-latest-small.zip)

2. Cliquer sur le bouton **Connect**

![](images/Copy%20Data%20HTTP%2004.png)

L'exécution de cette activité va permettre de télécharger le fichier ZIP [ml-latest-small.zip](https://files.grouplens.org/datasets/movielens/ml-latest-small.zip) et venir le placer dans le dossier **Files** du Lakehouse :

1. Depuis l'interface du Lakehouse (*Demo_LK*) utilisé dans ce tutoriel
    
2. Cliquer sur **Files** dans le volet de gauche du Lakehouse

3. Dans l'aperçu, vous devez retrouver le fichier ZIP qui a été téléchargé

![](images/View%20Lakehouse%2000.png)

## Extraire un fichier ZIP

A présent, nous allons présenter comment mettre en place une activité **Copy data** pour extraire les fichiers du ZIP qui a été téléchargé. Commencer par créer une nouvelle activité **Copy data** comme nous l'avons fait précédemment. Le symbole de l'activité **Copy data** comporte une flèche en bas à droite, cliquer dessus et faire glisser vers la nouvelle activité **Copy data** qui vient d'être ajoutée. A cette étape, vous devriez avoir un pipeline qui ressemble à ceci :

![](images/View%20Pipeline%2000.png)

Voyons maintenant comment définir les paramètres de cette activité **Copy data** en suivant les étapes suivantes :

- **Etape 1 : Définition des paramètres General**

    1. Revenir dans l'interface du Pipeline de données - *Download and Extract ZIP File*

    2. Cliquer sur l'icône de cette activité **Copy data**

    3. Se rendre dans le menu **General**

    4. Rentrer un nom pour cette activité dans le champ **Name**. Dans notre exemple, nous la nommons Extract ZIP File.

![](images/Copy%20Data%20Unzip%2000.png)

- **Etape 2 : Définition des paramètres Source**

1. Se rendre dans le menu **Source**

2. Dans le champ **Connexion**, choisir le Lakehouse qui a été créé pour ce projet (*Demo_LK*)
    
3. Dans le champ **Root folder**, choisir l'option **Files**

4. Dans le champ **File path type**, choisir l'option **File path**
    
5. Dans le champ **File path**, cliquer sur **Browse** puis depuis l'explorateur de fichier choisir le fichier [ml-latest-small.zip](https://files.grouplens.org/datasets/movielens/ml-latest-small.zip)  dans le Lakehouse

6. Depuis les options avancées **Advanced**, décocher l'option **Delete files after completion**

7. Depuis les options avancées **Advanced**, décocher l'option **Preverse zip file name as folder**

![](images/Copy%20Data%20Unzip%2001.png)

L'option de suppression du fichier après la tâche souhaitée (**Delete files after completion**) n'est possible que dans le cas d'une simple copie du fichier ZIP et non d'une extraction comme ce qui est le cas ici. Enfin pour permettre l'extraction du fichier ZIP, il est nécessaire de définir avec précision le format pour cela suivre les étapes suivantes :

1. Dans le champ **File format**, choisir **Binary**

2. Cliquer sur **Settings** ce qui va ouvrir la fenêtre **File format Settings**

3. Dans le champ **Compression type**, choisir l'option **ZipDeflate (.zip)**

4. Dans le champ **Compression level**, choisir l'option **Optimal**

5. Enfin cliquer sur le bouton **OK** pour fermer cette fenêtre

![](images/Copy%20Data%20Unzip%2002.png)

- **Etape 3 : Définition des paramètres Destination**

1. Se rendre dans le menu **Destination** de l'activité
    
2. Dans le champ **Connection**, choisir le Lakehouse créé pour ce projet
    
3. Dans le champ **Root folder**, choisir l'option **Files**

![](images/Copy%20Data%20Unzip%2003.png)

Le champ **File path** est laissé vide ce qui va conduire à ce que le contenu du fichier ZIP soit extrait dans un répertoire du même nom que le fichier source.

Après l'exécution de cette activité, nous pouvons observer depuis le Lakehouse les choses suivantes :

1. Un répertoire ml-latest-small dans le dossier **File** du Lakehouse

2. Les fichiers extraits du fichier ZIP

![](images/View%20Lakehouse%2001.png)

## Exécution du Pipeline de Données

A ce stade, nous allons pouvoir exécuter le Pipeline que nous venons de créer, en suivant, les étapes suivantes :

- **Etape 1 : Valider le Pipeline de données**

    1. Depuis l'interface du Pipeline, cliquer sur le bouton **Valider**
    
    2. Dans le volet de gauche, vous pourrez vérifier que le Pipeline est valide ou le cas échéant les erreurs à corriger avant de pouvoir lancer l'exécution du Pipeline

    3. Cliquer sur le bouton **Exécuter** si aucune erreur n'est détectée

![](images/Run%20Pipeline%2000.png)

- **Etape 2 : Exécuter le Pipeline de données**

1. Depuis l'interface du Pipeline, aller dans le menu Output

2. Suivre les états d'exécution des activités (**Queued**, **Processed**, **Succeeded**)

![](images/Run%20Pipeline%2001.png)

## Aperçu des données dans le Lakehouse

A présent, nous pouvons observer le contenu des fichiers qui ont été extraits. Depuis l'interface du Lakehouse, suivre les étapes suivantes :

1. Sélectionner le dossier *ml-latest-small* dans lequel les fichiers ont été extraits

2. Sélectionner l'un des fichiers extraits. Dans l'image ci-dessous, nous avons choisi le fichier *ratings.csv*

3. Sélectionner l'option **Table view**

4. Dans les options **View settings**, sélectionner **First row as header**

![](images/View%20Lakehouse%2005.png)

## Conclusion

Dans cet article, nous avons montrer comment extraire et charger des données depuis des fichiers ZIP directement dans votre environnement Fabric. Dans l'approche proposée, un pipeline de données Fabric fournit les outils nécessaires pour traiter efficacement vos archives compressées avec une approche No-Code.



