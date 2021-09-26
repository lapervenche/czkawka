# Installation de Czkawka
## conditions
### Linux
Si vous utilisez Snap, Flatpak ou Appimage, vous pouvez ignorer cette section.

Pour l'interface graphique de Czkawka, vous devez au moins avoir installé `GTK 3.22` et également `Alsa` (pour trouver des fichiers de musique cassés, fonction désactivée par défaut) sur votre pc. 
 
Il devrait être installé par défaut sur toutes les distributions les plus populaires.
#### Ubuntu/Debian
```
sudo apt install libgtk-3-dev
```
#### Fedora/CentOS
```
sudo yum install gtk3-devel glib2-devel
```
#### Void Linux (CLI only)
```
sudo xbps-install gcc pkg-config alsa-lib-devel
```

### macOS
Actuellement, vous devez installer manuellement les bibliothèques `GTK 3` et le thème Adwaita.
Ils sont chargés dynamiquement à partir du système d'exploitation ( nous avons besoin d'aide pour utiliser les liens statiques ). 
Une façon très simple de le faire est d'utiliser [Homebrew](https://brew.sh/). Installation dans le terminal:
```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install gtk+3 adwaita-icon-theme
```
Après cela, allez à l'emplacement où vous avez téléchargé Czkawka et ajoutez l'autorisation `executable` à ce fichier.
```shell
chmod +x mac_czkawka_gui
```
À la fin, exécutez-le :
```shell
./mac_czkawka_gui
```

### Les fenêtres
Par défaut, toutes les bibliothèques nécessaires sont fournies avec l'application.
A l'intérieur du fichier `windows_czkawka_gui.zip`,Si vous compilez l'application ou déplacez simplement  `czkawka_gui.exe`,vous devrez installer le runtime `GTK 3` à partir d'ici [**d'ici**](https://github.com/tschoonj/GTK-for-Windows-Runtime-Environment-Installer/releases)..

## Installation
### Fichiers binaires précompilés
Des exécutables prêts à l'emploi pour Linux, Windows et macOS sont disponibles [**ici**](https://github.com/qarmin/czkawka/releases/).  
Si l'application ne s'exécute pas lorsque vous cliquez sur le lanceur, exécutez-la via un terminal. 
Vous n'avez pas besoin de bibliothèques supplémentaires pour CLI Czkawka.

### Nightly Builds
Les artefacts de chaque commit peuvent être téléchargés [**ici**](https://github.com/qarmin/czkawka/actions)

### Appimage
Les fichiers Appimage sont disponibles dans la page de publication - [**GitHub releases**](https://github.com/qarmin/czkawka/releases/)  
Cette version est livrée avec son propre thème.  
Il y a aussi le petit problème de ne pas pouvoir ouvrir 2 images à la fois.

### Cargo
La méthode la plus simple pour installer Czkawka consiste à utiliser la commande `cargo`. Pour le compiler, vous devez obtenir toutes les conditions requises dans la  [section compilation](Compilation.md).

```
cargo install czkawka_gui
cargo install czkawka_cli
```
Vous pouvez mettre à jour le package avec la même commande.

### Snap
```
sudo snap install czkawka
```
Par défaut, Snap ne peut accéder qu'aux fichiers de votre répertoire personnel. Vous devez autoriser czkawka à accéder à tous les lecteurs :

```
sudo snap connect czkawka:removable-media
```

L'entrée du magasin Snap peut être trouvée [**ici**](https://snapcraft.io/czkawka).

De nouvelles versions sont disponibles dans la branche Edge, mais elles peuvent être un peu instables,bien que cela se produise très rarement car je ne pousse pas de code non testé.

### Flatpak
```
flatpak install flathub com.github.qarmin.czkawka
```
La page Flathub avec Czkawka peut être trouvée [**ici**](https://flathub.org/apps/details/com.github.qarmin.czkawka)

#
#

**Paquets non officiels, qui peuvent ne pas toujours fournir la dernière version de Czkawka.**

### PPA - Debian/Ubuntu (unofficial)
```
sudo add-apt-repository ppa:xtradeb/apps
sudo apt-get update
sudo apt-get install czkawka
```

### AUR - Arch Linux Package (unofficial)
Czkawka est également disponible dans l'AUR d'Arch Linux à partir duquel il peut être facilement installé.
```
yay -Syu czkawka-git
```
ou
```
yay -Syu czkawka-gui-bin
yay -Syu czkawka-cli-bin
```

Informations sur le paquet - https://aur.archlinux.org/packages/?O=0&SeB=nd&K=czkawka&outdated=&SB=n&SO=a&PP=50&do_Search=Go

### Docker image (unofficial)
L'image du docker Czkawka est disponible [**ici**](https://github.com/jlesage/docker-czkawka)
