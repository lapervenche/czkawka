![com github qarmin czkawka](https://user-images.githubusercontent.com/41945903/102616149-66490400-4137-11eb-9cd6-813b2b070834.png)

**Czkawka** (_tch•kav•ka_, hiccup) est une application simple, rapide et gratuite pour supprimer les fichiers inutiles de votre ordinateur.

## Caractéristiques
- Écrit dans la mémoire en toute sécurité Rust
- Étonnamment rapide - grâce à l'utilisation d'algorithmes plus ou moins avancés et au multithreading
- Gratuit, Open Source sans publicité
- Multiplateforme - fonctionne sur Linux, Windows et macOS
- Prise en charge du cache - la deuxième analyse et les analyses suivantes devraient être beaucoup plus rapides que la première
- Interface CLI - pour une automatisation facile
- Interface graphique - utilise GTK 3 moderne et ressemble à FSlint
- Option de recherche riche - permet de définir des répertoires inclus et exclus absolus, un ensemble d'extensions de fichiers autorisées ou des éléments exclus avec le `*` caractère générique
- Plusieurs outils à utiliser : 
  - DDoublons - Trouve les doublons en fonction du nom de fichier, de la taille, du hachage, du hachage du premier Mo d'un fichier
  - Dossiers vides - Trouve les dossiers vides à l'aide d'un algorithme avancé
  - Gros Fichiers - Trouve le nombre fourni des plus gros fichiers dans un emplacement donné
  - Fichiers vides - Recherche les fichiers vides sur le lecteur
  - Fichiers temporaires - Trouve les fichiers temporaires
  - Images similaires - Trouve des images qui ne sont pas exactement les mêmes (résolution différente, filigranes)
  - Zeroed Fichiers - Trouve les fichiers qui sont remplis de zéros (généralement corrompus)
  - Même musique - Recherche de la musique avec le même artiste, album, etc.
  - Liens symboliques invalides - Affiche les liens symboliques qui pointent vers des fichiers/répertoires inexistants
  - Fichiers cassés - Trouve les fichiers avec une extension invalide ou qui sont corrompus

<!-- The GIF thingy -->
![Czkawka](https://user-images.githubusercontent.com/41945903/104711404-9cbb7400-5721-11eb-904d-9677c189f7ab.gif)

## Comment l'utiliser?
Vous pouvez trouver les instructions sur la façon d'utiliser Czkawka [**ici**](instructions/Instruction.md).

## Installation
Instructions d'installation avec liens de téléchargement que vous pouvez trouver [**ici**](instructions/Installation.md).

## Compilation
Si vous souhaitez essayer de développer Czkawka ou simplement utiliser la dernière fonctionnalité disponible, vous pouvez consulter les [**instructions de compilation **](instructions/Compilation.md).

## Repères

Étant donné que Czkawka est écrit en Rust et qu'il vise à être une alternative plus rapide à FSlint ou DupeGuru qui sont écrits en Python, nous devons comparer la vitesse de ces outils.

Testé initialement sur un SSD de 256 Go et un CPU i7-4770.

Disque préparé et lancement d'un test sans aucune exception de dossier et en ignorant les liens durs désactivés qui contenaient 363 215 fichiers, prenaient 221,8 Go et avaient 62093 fichiers en double dans 31790 groupes qui occupaient 4,1 Go.

Défini de la taille de fichier minimale à vérifier sur 1 Ko sur tous les programmes.

| Application                         | Temps d'exécution |
|:-----------------------------------:|:-----------------:|
| FSlint 2.4.7   (Première exécution) |    86s            |
| FSlint 2.4.7   (Deuxième exécution) |    43s            |
| Czkawka 3.0.0  (Première exécution) |    8s             |
| Czkawka 3.0.0  (Deuxième exécution) |     7s            |
| DupeGuru 4.1.1 (Première exécution) |    22s            |
| DupeGuru 4.1.1 (Deuxième exécution) |    21s            |

Utilisation de Mprof pour vérifier l'utilisation de la mémoire de FSlint et DupeGuru, et Heaptrack pour Czkawka.

| Application            | Ram au ralenti | Utilisation maximale de la RAM opérationnelle | Stabilisé après recherche |
|:----------------------:|:--------------:|:---------------------------------------------:|:-------------------------:|
| FSlint 2.4.7           |       62 MB    |                     164 MB                    | 158 MB                    |
| Dupeguru 4.1.1         |       90 MB    |                      170 MB                   | 166 MB                    |
| Czkawka 3.0.0          |       12 MB    |                      122 MB                   | 60 MB                     |


Dans Dupeguru, activation de la vérification des images avec des dimensions différentes pour correspondre au comportement de Czkawka. Les deux applications utilisent un mécanisme de mise en cache, la deuxième analyse est donc très rapide.

Images similaires qui vérifient 10949 fichiers qui occupaient 6,6 Go

| Application                         | Temps de balayage |
|:-----------------------------------:|:-----------------:|
| Czkawka 3.0.0  (Première exécution) |         276s      |
| Czkawka 3.0.0  (Deuxième exécution) |         1s        |
| DupeGuru 4.1.1 (Première exécution) |         539s      |
| DupeGuru 4.1.1 (Deuxième exécution) |         1s        |

Images similaires qui vérifient 349 fichiers image qui occupaient 1,7 Go

| Application                         | Temps de balayage|
|:-----------------------------------:|:-----------------|
| Czkawka 3.0.0  (Première exécution) |        54s       |
| Czkawka 3.0.0  (Deuxième exécution) |        1s        |
| DupeGuru 4.1.1 (Première exécution) |        55s       |
| DupeGuru 4.1.1 (Deuxième exécution) |        1s        |

## Comparaison avec d'autres outils

Bleachbit est un maître dans la recherche et la suppression de fichiers temporaires, tandis que Czkawka ne trouve que les plus basiques. Ces deux applications ne doivent donc pas être comparées directement ou être considérées comme une alternative l'une à l'autre.

|                                   | Czkawka     | FSlint     | DupeGuru          | Bleachbit   |
|:---------------------------------:|:-----------:|:----------:|:-----------------:|:-----------:|
| Langue                            | Rust        | Python     | Python/Obj-C      | Python      |
| Système d'exploitation            | Lin,Mac,Win | Lin        | Lin,Mac,Win       | Lin,Mac,Win |
| Framework                         | GTK 3       | PyGTK2     | Qt 5 (PyQt)/Cocoa | PyGTK3      |
| Recherche de doublons             | •           | •          | •                 |             |
| Fichiers vides                    | •           | •          |                   |             |
| Dossiers vides                    | •           | •          |                   |             |
| Fichiers temporaires              | •           | •          |                   | •           |
| Gros fichiers                     | •           |            |                   |             |
| Images similaires                 | •           |            | •                 |             |
| Fichiers mis à zéro               | •           |            |                   |             |
| Doublons de musique (tags)        | •           |            | •                 |             |
| Liens symboliques invalides       | •           | •          |                   |             |
| Fichiers cassés                   | •           |            |                   |             |
| Conflit de noms                   | •           | •          |                   |             |
| Paquets installés                 |             | •          |                   |             |
| Noms invalides                    |             | •          |                   |             |
| Mauvais identifiant               |             | •          |                   |             |
| binaires non dépouillés           |             | •          |                   |             |
| Espace redondant                  |             | •          |                   |             |
| Écraser des fichiers              |             | •          |                   | •           |
| Plusieurs langues (po)            |             | •          | •                 | •           |
| Prise en charge du cache          | •           |            | •                 |             |
| En développement actif            | Yes         | No         | Yes               | Yes         |

## Autres applications
Il existe de nombreuses applications similaires à Czkawka sur Internet, qui font certaines choses mieux et d'autres moins bien.
- [DupeGuru](https://github.com/arsenetar/dupeguru) - Beaucoup d'options à personnaliser
- [FSlint](https://github.com/pixelb/fslint) - Un peu obsolète, mais dispose de nombreux outils utiles
- [Fclones](https://github.com/pkolaczk/fclones) - L'un des outils les plus rapides pour trouver des doublons, mais uniquement en CLI

## Contributions
Les contributions à ce référentiel sont les bienvenues.

Vous pouvez aider en créant :
- Rapports de bogues - fuites de mémoire, comportement inattendu, plantages
- Propositions de fonctionnalités - proposition de modifier/ajouter/supprimer certaines fonctionnalités
- Pull Requests - implémenter vous-même une nouvelle fonctionnalité ou corriger des bogues. Si le changement est plus important, alors c'est une bonne idée d'ouvrir un nouveau problème pour discuter des changements.
- Documentation - Il existe une [instruction](instructions/Instruction.md) que vous pouvez améliorer.

Vous pouvez aussi aider en faisant différentes choses :
- Création d'articles de texte - [LinuxUprising](https://www.linuxuprising.com/2021/03/find-and-remove-duplicate-files-similar.html) ou [Ubunlog](https://ubunlog.com/en/czkawka-finds-and-removes-empty-and-broken-duplicate-files/)
- Ajout de Czkawka aux référentiels - [Alpine Linux](https://pkgs.alpinelinux.org/packages?name=czkawka&branch=edge) ou [NixOS](https://github.com/NixOS/nixpkgs/pull/116441) ou [OpenMandriva](https://github.com/OpenMandrivaAssociation/czkawka)
- Création de vidéos - [First Video](https://www.youtube.com/watch?v=CWlRiTD4vDc) ou [Tutorial Spanish](https://www.youtube.com/watch?v=V9x-pHJRmKY)
- Recommander Czkawka à d'autres

## Nom
Czkawka est un mot polonais qui signifie hoquet .

Le nom à été choisi par l'auteur du script original parce que je voulais entendre des personnes parlant d'autres langues le prononcer, alors n'hésitez pas à l'épeler comme vous le souhaitez.

Ce nom n'est pas aussi mauvais qu'il n'y paraît, car il pensait aussi utiliser des mots comme żółć , gżegżółka ou żołądź , mais il a abandonné ces idées car elles contenaient des caractères polonais, ce qui compliquerait la recherche du projet.

Au début de la création du programme, si la réponse concernant le nom était unanimement négative, il se préparait à un éventuel changement de nom du programme, et les avis étaient extrêmement mitigés.

## License
Le code est distribué sous licence MIT.

L'icône a été créé par [jannuary](https://github.com/jannuary) et sous licence CC-BY-4.0.

Le thème sombre de Windows est utilisé à partir du [référentiel AdMin](https://github.com/nrhodes91/AdMin) avec une licence MIT.

Le programme est entièrement gratuit à utiliser.

"Gratis to uczciwa cena" - "Gratuit est un juste prix"

## Remerciements à

Un grand merci à Pádraig Brady, créateur du fantastique FSlint, car sans son travail, je ne créerais pas cet outil.

Merci également à toutes les personnes qui créent des correctifs pour ce programme, le rendent disponible sur d'autres systèmes, créent des vidéos, des articles à ce sujet, etc.

## Don
Si vous utilisez l'application, le créateur original du script apprécierait un don pour son développement ultérieur, qui peut être fait [ici](https://github.com/sponsors/qarmin).
