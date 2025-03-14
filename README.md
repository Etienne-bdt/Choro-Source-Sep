# Choro source separation - Rendu de projet long

## Introduction

Ceci est le ReadMe pour notre projet long sur la musique choro. 

## Organisation du projet

Le projet est organisé en plusieurs dossiers :
 - data : contient les bases de données

## Lancement de l'entrainement du modèle

Ici il faut utiliser dora, les commandes usuelles sont sur le [Github du projet demucs](https://github.com/adefossez/demucs/).

```
    source /projects/choro/demucs-env/bin/activate
    
    cd /projects/choro/demucs/demucs

    python -m demucs.separate --repo ./release_models -n htdemucs mixture.mp3
```

### Poids des modèles

Les poids des modèles sont disponibles dans release models. Pour exporter (et les utiliser pour séparer des pistes), il faut utiliser la commande suivante :
```
    python -m tools.export --repo ./release_models hash
```

Nous vous laissons les poids des modèles que nous avons entrainé dans le dossier release_models :
 - htdemucs : modèle entrainé sur la base de données stéréo
 - htdemucsmono : modèle entrainé sur la base de données mono avec un découpage automatique
 - htdemucsmonomanual : modèle entrainé sur la base de données mono avec un découpage manuel

À utiliser avec la commande ci-dessous:
```
    python -m demucs.separate --repo ./release_models -n htdemucs mixture.mp3
```

Pour entrainer un modèle, il faut utiliser les fichiers de configuration dans le dossier conf

### Dataset 

La configuration se fait dans les fichiers `conf/dset/fichier.yaml`

### Variante

La configuration se fait dans les fichiers `conf/variant/fichier.yaml`

### Entrainement 

Une fois les configurations faites, il suffit de lancer une commande (ne pas oublier le VENV et de cd dans choro/demucs/demucs)

```
    python -m demucs.train dset=fichier1.yaml variant=fichier2.yaml
```

### Fichiers de configuration

Nous laissons à votre disposition les fichiers de configuration que nous avons utilisé pour notre projet.
Vous pouvez les retrouver dans le dossier `conf`. Nous vous laissons :
 - bdd_stereo.yaml : configuration pour la base de données stéréo
 - bdd_mono_auto.yaml : configuration pour la base de données mono
 - bdd_mono_manual.yaml : configuration pour la base de données mono avec un autre découpage

 Pour les variantes, nous vous laissons :
 - htdemucs.yaml : configuration pour le modèle htdemucs
Attention : il y a une ligne pour le chemin des données qu'il faut peut être changer dans les variantes.

## Checkpoints 

Les checkpoints sont sauvegardés dans le dossier outputs, ils sont dans le hash de l'entrainement qui est donné au moment du démarrage de l'entrainement par Dora.

## Remerciements

Merci beaucoup à vous pour votre aide et ce projet ! Nous espérons que le travail que nous avons fourni vous sera utile.

## Note 

Si vous avez des problème pour lancer quelque chose, pensez à utiliser :
```
    pip install -r requirements.txt --user
```

Dans le dossier demucs pour installer les dépendances nécessaires.
Il est possible qu'elle soit manquante dans le VENV.