# Utilisation du logiciel

- [Interface graphique](#gui-gtk)
- [Interface graphique](#interface-graphique-GTK)
- [CLI](#cli)
- [Fichiers de configuration/cache](#configcache-files)
- [Trucs, astuces et bugs connus](#tips-tricks-and-known-bugs)
- [Outils](#outils)

Czkawka pour l'instant contient deux fronts indépendants - l'interface terminale et graphique qui partagent le module de base.
L'utilisation du langage Rust sans que le code soit dangereux aide à créer une application sécurisée, rapide et nécessitant peu de ressources. Ce code a également un bon soutien pour le multi-threading.

## 
Interface graphique GTK
<img src="https://user-images.githubusercontent.com/41945903/103002387-14d1b800-452f-11eb-967e-9d5905dd6db5.png" width="800" />

### Présentation de l'interface graphique
L'interface graphique est construite à partir de différentes pièces :

Rouge - Paramètres du programme, contient des informations sur les répertoires inclus/exclus que l'utilisateur peut vouloir vérifier. En outre, il existe un onglet avec les extensions autorisées, qui permet aux utilisateurs de choisir le type de fichiers qu'ils souhaitent vérifier. La catégorie suivante est les éléments exclus, ce qui permet d'ignorer un chemin spécifique en utilisant un *caractère générique, ce /home/ra*qui signifie que, par exemple, /home/rafal/sera ignoré mais pas /home/czkawka/. Le dernier est l'onglet Paramètres qui permet d'enregistrer la configuration du programme, de le réinitialiser et de le charger si nécessaire.

Vert - Cela permet de choisir l'outil que nous voulons utiliser.

Bleu - Voici les paramètres de l'outil actuel, que nous voulons / devons configurer

Rose - Fenêtre dans laquelle les résultats de la recherche sont imprimés

Jaune - Boîte avec des boutons comme Search(commence la recherche avec l'outil actuellement sélectionné), Hide Text View(masque la zone de texte en bas avec une superposition blanche), Symlink(crée un lien symbolique vers le fichier sélectionné), Select(affiche les options pour sélectionner des lignes spécifiques), Delete(supprime les fichiers sélectionnés) , Save(enregistrer pour archiver le résultat de la recherche) - certains boutons ne sont visibles que lorsqu'au moins un résultat est visible.

Marron - Petit champ informatif pour afficher des informations, par exemple sur le nombre de fichiers en double trouvés

Blanc - Fenêtre de texte pour afficher les erreurs/avertissements possibles, par exemple en cas d'échec de la suppression du dossier en raison de l'absence d'autorisations, etc.

Il existe également une option pour voir les aperçus d'images dans l'outil Images similaires.

<img src="https://user-images.githubusercontent.com/41945903/103025544-50ca4480-4552-11eb-9a54-f1b1f6f725b1.png" width="800" />

### Boutons d'action

Il y a plusieurs boutons qui font différentes actions :

- Rechercher - démarre la recherche et affiche la boîte de dialogue de progression
- Arrêter - bouton dans la boîte de dialogue en cours, permet d'arrêter facilement la tâche en cours. Parfois, cela peut prendre quelques secondes jusqu'à ce que toutes les opérations atomiques se terminent et que l'interface graphique redevienne réactive
- Sélectionner - permet de sélectionner plusieurs entrées à la fois
- Supprimer - supprime entièrement toutes les entrées sélectionnées
- Lien symbolique - crée un lien symbolique vers les fichiers sélectionnés (le premier fichier est menacé comme original et le reste deviendra des liens symboliques)
- Enregistrer - enregistrer l'état initial des résultats
- Hamburger (lignes parallèles) - utilisé pour afficher/masquer le panneau de texte inférieur qui affiche les avertissements/erreurs
- Ajouter (répertoires) - ajoute des répertoires à inclure ou à exclure
- Supprimer (répertoires) - supprime les répertoires à rechercher ou à exclure
- Ajout manuel (répertoires) - permet de saisir en tapant des répertoires (peut être utilisé pour entrer des répertoires non visibles dans le gestionnaire de fichiers)
- Enregistrer la configuration actuelle - enregistre la configuration actuelle de l'interface graphique dans le fichier de configuration
- Charger la configuration - charge la configuration du fichier et remplace la configuration actuelle de l'interface graphique
- Réinitialiser la configuration - réinitialise la configuration actuelle de l'interface graphique aux valeurs par défaut

### Ouverture/Manipulation de fichiers

Il est possible d'ouvrir les fichiers sélectionnés en double-cliquant dessus.

Pour ouvrir plusieurs fichiers, sélectionnez simplement les fichiers souhaités avec la touche CTRL enfoncée et toujours en cliquant sur cette touche, double-cliquez sur les éléments sélectionnés avec le bouton gauche de la souris.

Pour ouvrir le dossier contenant le fichier sélectionné, cliquez simplement deux fois dessus avec le bouton droit de la souris.


## CLI
L'interface CLI Czkawka est idéale pour automatiser certaines tâches telles que la suppression de répertoires vides.

Pour obtenir des informations générales sur son utilisation, essayez simplement d'ouvrir czkawka_cli dans la console `czkawka_cli`

<img src="https://user-images.githubusercontent.com/41945903/103018271-3d64ac80-4545-11eb-975c-2132f2ccf66f.png" width="800" />

Vous devriez voir beaucoup d'exemples d'utilisation de cette application.

Si vous souhaitez obtenir des informations plus détaillées sur certains outils, ajoutez simplement après son nom `-h` ou `--help` pour obtenir plus de détails.

<img src="https://user-images.githubusercontent.com/41945903/103018151-0a221d80-4545-11eb-97b2-d7d77b49c735.png" width="800" />

Par défaut, tous les outils n'écrivent que sur les résultats dans la console, mais il est possible avec des arguments spécifiques de supprimer certains fichiers/arguments ou de les enregistrer dans un fichier.


## Fichiers de configuration/cache
Actuellement, Czkawka stocke quelques fichiers de configuration et de cache sur le disque :
- `czkawka_gui_config.txt` - stocke la configuration de l'interface graphique qui peut être chargée au démarrage
- `cache_similar_image.txt` - stocke les données de cache et les hachages qui peuvent être utilisés ultérieurement sans avoir à recalculer le hachage de l'image - la modification de ce fichier peut provoquer des plantages de l'application.

- `cache_broken_files.txt` - stocke les données de cache des fichiers cassés
- `cache_duplicates_Blake3.txt` - stocke les données de cache des fichiers dupliqués, pour ne pas subir un impact trop important sur les performances lors de l'enregistrement/du chargement du fichier, seuls les fichiers déjà entièrement hachés de plus de 5 Mo sont stockés. Des fichiers similaires remplacés Blake3par exemple par SHA256peuvent être affichés, lorsque la prise en charge de nouveaux hachages sera introduite dans Czkawka.


Les fichiers de configuration se trouvent dans ce chemin :

Linux - `/home/username/.config/czkawka`  
Mac - `/Users/username/Library/Application Support/pl.Qarmin.Czkawka`  
Windows - `C:\Users\Username\AppData\Roaming\Qarmin\Czkawka\config`

Le cache devrait être ici :

Linux - `/home/username/.cache/czkawka`  
Mac - `/Users/Username/Library/Caches/pl.Qarmin.Czkawka`  
Windows - `C:\Users\Username\AppData\Local\Qarmin\Czkawka\cache`

## Trucs, astuces et bugs connus
- **Ajout manuel de plusieurs répertoires**  
Vous pouvez éditer manuellement le fichier de configuration `czkawka_gui_config.txt` et ajouter/supprimer/modifier des répertoires comme vous le souhaitez. Après avoir défini les valeurs requises, la configuration doit être chargée dans Czkawka.

- **Vérification lente d'un petit nombre d'images similaires**  
Si vous avez vérifié avant un grand nombre d'images (plusieurs dizaines de milliers) et qu'elles sont toujours présentes sur le disque, les informations requises sur chacune d'entre elles sont chargées et enregistrées dans le cache, même si vous travaillez avec seulement quelques fichiers image. Vous pouvez renommer le fichier cache `cache_similar_image.txt`(pour pouvoir l'utiliser à nouveau) ou le supprimer - le cache se régénérera alors mais avec un plus petit nombre d'entrées et de cette façon, il devrait se charger et enregistrer beaucoup plus rapidement.

- **Toutes les colonnes ne sont pas visibles**
  Pour l'instant, il est possible que certaines colonnes ne soient pas visibles lorsque certaines sont trop larges. Il y a 2 solutions de contournement pour le moment
    - La vue peut être défilée via la barre de défilement horizontale
    - La taille des autres colonnes peut être réduite
  
  Ceci est géré via https://github.com/qarmin/czkawka/issues/169

![AA](https://user-images.githubusercontent.com/41945903/125684641-728e264a-34ab-41b1-9853-ab45dc25551f.png)

# Outils

### Recherche de doublons

Duplicate Finder permet de rechercher des fichiers et de les regrouper selon un critère prédéfini :

- **Par nom** - Compare et regroupe les fichiers par nom, par exemple, `/home/john/cats.txt`sera traité comme un doublon d'un fichier nommé `/home/lucy/cats.txt`. C'est la méthode la plus rapide, mais elle est très peu fiable et ne doit pas être utilisée à moins que vous ne sachiez ce que vous faites.


- **Par taille** - Compare et regroupe les fichiers par leur taille (en octets et correspondances parfaites uniquement). Il est aussi rapide que le mode précédent et donne généralement de meilleurs résultats avec les doublons, mais je ne recommande pas non plus de l'utiliser si vous ne savez pas ce que vous faites.


- **Par hachage* - Un mode contenant une vérification du hachage (hachage cryptographique) d'un fichier donné qui détermine avec une grande probabilité si les fichiers sont identiques.


  C'est le moyen le plus lent, mais presque sûr à 100%, de comparer les fichiers pour qu'ils soient identiques.

  Comme le hachage n'est vérifié qu'à l'intérieur de groupes de fichiers de même taille, il est pratiquement impossible que deux fichiers différents soient considérés comme identiques.


  Il se compose de 3 étapes :
    - Regrouper des fichiers de taille identique - vous permet de jeter des fichiers de taille unique, qui sont déjà connus pour n'avoir aucun doublon à ce stade.

    - Vérification PreHash - Chaque groupe de fichiers de taille identique est placé dans une file d'attente en utilisant tous les threads du processeur (chaque action du groupe est indépendante des autres). Dans chacun de ces groupes, un petit fragment de chaque fichier (2 Ko) est chargé à son tour puis haché. Tous les fichiers dont les hachages partiels sont uniques au sein du groupe en sont supprimés. L'utilisation de cette étape me permet généralement de réduire de moitié le temps de recherche de doublons.

    - Vérification du hachage - Après avoir laissé les fichiers qui ont le même début dans les groupes, vous devez maintenant vérifier tout le contenu du fichier pour vous assurer qu'ils sont identiques.

- **Par hashmb** - Fonctionne de la même manière que via hash, seulement dans la dernière phase, il ne calcule pas le hachage de l'ensemble du fichier mais seulement de son premier mégaoctet. Il est parfait pour une recherche rapide d'éventuels fichiers en double.

### Fichiers vides
La recherche de fichiers vides est simple et rapide, car il suffit de vérifier les métadonnées du fichier et sa longueur.

### Répertoires vides
Au début, une entrée spéciale est créée pour chaque répertoire contenant - le chemin parent (uniquement s'il ne s'agit pas d'un dossier directement sélectionné par l'utilisateur) et un indicateur pour indiquer si le répertoire donné est vide (au début chacun est défini être potentiellement vide).

Tout d'abord, les dossiers définis par l'utilisateur sont placés dans le pool de dossiers à vérifier.

Chaque élément est vérifié pour voir s'il est :
- dossier - ce dossier est ajouté à la file d'attente de vérification comme vide possible - `FolderEmptiness::Maybe`
- autre chose - le dossier donné est "empoisonné" avec le drapeau`FolderEmptiness::No`, indiquant que le dossier n'est plus vide. Ensuite, chaque dossier contenant directement ou indirectement le fichier est également empoisonné avec le drapeau`FolderEmptiness::No`.

Exemple : il y a 4 dossiers cochés qui peuvent être vides `/cow/`, `/cow/ear/`, `/cow/ear/stack/`, `/cow/ear/flag/`.

Le dernier dossier contient un fichier, ce qui signifie qu'il `/cow/ear/flag`n'est pas vide ainsi que tous ses parents - `/cow/ear/`et `/cow/`, mais qu'il `/cow/ear/stack/`peut toujours être vide..

Enfin, tous les dossiers avec le drapeau `FolderEmptiness::Maybe` sont par défaut vides.

### Gros fichiers
Pour chaque fichier à l'intérieur du chemin donné, sa taille est lue, puis après avoir trié la liste, par exemple les 50 plus gros, les fichiers sont affichés.

### Fichiers temporaires
La recherche de fichiers temporaires consiste uniquement à comparer leurs extensions avec une liste préalablement préparée.

```
["#", "thumbs.db", ".bak", "~", ".tmp", ".temp", ".ds_store", ".crdownload", ".part", ".cache", ".dmp", ".download", ".partial"]
```

### Fichiers mis à zéro
Les fichiers mis à zéro sont très souvent le résultat de téléchargements de fichiers incorrects, par exemple.

Leur recherche comprend 3 étapes:
- Collecte d'une liste de tous les fichiers d'une taille supérieure à 0
- Au début, 64 octets de chaque fichier sont vérifiés pour éliminer la grande majorité des fichiers non nuls sans pertes de performances majeures.
- L'étape suivante consiste à vérifier le reste du fichier avec des parties plus grandes (32 Ko)
- 
### Liens symboliques invalides
Pour trouver des liens symboliques invalides, nous devons d'abord trouver des liens symboliques.

Après les avoir recherchés, vous devez vérifier vers quel élément il pointe et s'il n'existe pas, ajoutez ce lien symbolique dans la liste des liens symboliques invalides, pointant vers un chemin inexistant.

Le deuxième mode consiste à détecter un lien symbolique récursif. Malheureusement, ce mode ne fonctionne pas et il affiche lors de son utilisation une erreur d'élément cible inexistant, mais il est implémenté en comptant les sauts du lien symbolique et après avoir dépassé un certain nombre (par exemple 20) on considère que le donné le lien symbolique est récursif.

### Même musique
Il s'agit d'un mode permettant de rechercher des fichiers musicaux identiques via des balises.

Le nombre de balises parmi lesquelles choisir est limité par une bibliothèque externe.

Tout d'abord, les fichiers musicaux avec l'une des extensions `[".mp3", ".flac", ".m4a"]` are collected.

Ensuite, pour chaque fichier musical, ses balises sont lues.

Ensuite, pour chaque balise sélectionnée par laquelle nous voulons rechercher des doublons, nous effectuons les étapes suivantes :
- Pour chaque fichier d'entrée, nous lisons la valeur de la balise actuellement vérifiée
- S'il est vide, on ignore le fichier, s'il a une valeur, on le jette dans un tableau dont la clé est cette valeur
- Après vérification de tous les fichiers, les tableaux contenant un seul élément sont supprimés
- Les fichiers restants sont utilisés comme données initiales pour vérifier la prochaine balise sélectionnée par l'utilisateur
- Après avoir vérifié toutes les balises, les résultats sont affichés en groupes

### Images similaires
C'est un outil pour trouver des images similaires qui diffèrent par exemple par le filigrane, la taille, etc.

L'outil collecte d'abord des images avec des extensions spécifiques qui peuvent être vérifiées -`[".jpg", ".jpeg", ".png", ".bmp", ".tiff", ".tif", ".pnm", ".tga", ".ff", ".gif", ".jif", ".jfi", ".ico", ".webp", ".avif"]`.

Les données mises en cache suivantes sont chargées à partir du fichier pour éviter de hacher deux fois le même fichier. 
The cache which points to non existing data is deleted automatically.

Le cache qui pointe vers des données non existantes est supprimé automatiquement.

Le hachage cryptographique (utilisé par exemple dans les chiffrements) pour des entrées similaires donne des sorties complètement différentes :   
11110 ==>  AAAAAB  
11111 ==>  FWNTLW  
01110 ==>  TWMQLA

Hash perceptif à des entrées similaires, donne des sorties similaires :   
11110 ==>  AAAAAB  
11111 ==>  AABABB  
01110 ==>  AAAACB


Les données de hachage calculées sont ensuite jetées dans un arbre spécial qui permet de comparer les hachages en utilisant la distance [Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance).

Ensuite, ces hachages sont enregistrés dans un fichier, pour pouvoir ouvrir les images sans avoir besoin de les hacher plusieurs fois.


Enfin, chaque hachage est comparé aux autres et si la distance entre eux est inférieure à la distance maximale spécifiée par l'utilisateur, les images sont considérées comme similaires et rejetées du pool d'images à rechercher.
### Fichiers cassés
Cet outil trouve les fichiers corrompus ou ayant une extension invalide.

Au début, les fichiers d'un groupe spécifique (image, archive, audio) sont collectés, puis ces fichiers sont ouverts.

Si une erreur se produit lors de l'ouverture d'un tel fichier, cela signifie que ce fichier est corrompu ou non pris en charge.

Seules certaines extensions de fichiers sont prises en charge, car je m'appuie sur des caisses externes. De plus, certains faux positifs peuvent être affichés (par exemple https://github.com/image-rs/jpeg-decoder/issues/130 ) alors ouvrez toujours le fichier pour vérifier s'il est vraiment cassé.
