# decodeur-morse-audio
Décodeur Morse pour les Fichier Audio WAV Neutre



# Decodeur Morse

Ce programme est en solution pour Le Décodage des Enregistrements Morse, dont les instructions peuvent être trouvées dans [Mon Profile GitHub][zhairi-azzeddine].

Le programme lit le fichier audio wav et génère le code morse décodé en sortie standard.

## Démarrage rapide

### Exigences
Pour l'instant, seul Python 3.10 est pris en charge.

###Installation

#### Etape 1 - installation de package nécessaire

Vous pouvez installer ce package depuis pip, avec

    pip install morse-audio-decoder

#### Etape 2 - Installation locale à partir des sources

Clonez le référentiel de code depuis votre ordinateur local sur linux, ou telecharger le directement de cette page:

    clone git https://github.com/zhairiazzeddine/decodeur-morse-audio.git

### Utilisation

Pour exécuter le script allez sur le dossier et ouvrir le CMD, Apres effectuez

    python -m decodeur_morse_audio "chemin du fichier en extension wav

    

où `WAVFILE` est le chemin d'accès au fichier audio à traiter.

Le programme décode le code morse audio dans l'argument WAVFILE et écrit la traduction sur la sortie standard.
Voir l'aide du programme avec l'indicateur de ligne de commande `-h` :

    $ décodeur-audio-morse -h
    utilisation : décodeur-audio-morse [-h] WAVFILE

    Lisez le fichier audio au format WAV, extrayez le code morse et écrivez le texte traduit dans la sortie standard.

    arguments de position :
    WAVFILE Fichier audio d'entrée

    choix :
    -h, --help afficher ce message d'aide et quittert

### Utilisation en Python

```python
from decodeur_morse_audio.morse import MorseCode

morse_code = MorseCode.from_wavfile("/path/to/file.wav")
out = morse_code.decode()
print(out)
```



### Restrictions

Ce décodeur a été testé et développé avec des entrées qui ont
- pas de bruit
- vitesse de frappe constante
- tonalité constante
- un seul canal d'entrée.

Si le décodeur devait être étendu à des entrées bruyantes présentant des différences majeures, il faudrait au moins les modifications suivantes.
- détection du pitch en temps de déplacement
- extraction du signal avec filtre passe-bande étroit, basé sur le pitch identifié
- détection de la vitesse de saisie (caractères/mots par minute)
- décodage par pas de temps plus petits, en tenant compte des changements de vitesse.

Le programme n'est pas non plus destiné à identifier des caractères uniques, car la précision sera moindre avec des entrées plus courtes.

## Développement

### Environnement

Exigences:
-Python 3.10
- Poésie (voir [instructions d'installation][poetry-install])

Dépendances :
-Numpy
- Scikit-learn

1. Installez les dépendances avec `poetry install`
2. Entrez dans l'environnement avec `poetry shell`


### Qualité et tests du code

Tout le code doit être formaté avec « black » :

    noir **/*.py

et qualité du code vérifiée avec `pylint` :

    pylint **/*.py

Les tests doivent être écrits en « pytest », ciblant une couverture de code pratique maximale. Les tests sont exécutés avec :

    test py

et couverture des tests vérifiée avec

    pytest --cov

En option, des rapports de couverture de test HTML peuvent être produits avec

    pytest --cov decodeur_morse_audio --cov-report html

