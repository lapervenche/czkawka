# Compilation de Czkawka à partir de codes sources

## Les Conditions
Programme  | Minimum  | Pourquoi
-----------|----------|------------------------------------------------------------
Rust       |   1.51   | Czkawka, aims to support the latest available version of Rust on Ubuntu 20.04
GTK        |   3.22   | Only for the `GTK` backend

Si vous souhaitez uniquement la version terminal sans interface graphique, ignorez simplement tous les packages contenant pour nom `gtk`.

#### Debian / Ubuntu
```shell
sudo apt install -y curl  # Needed by Rust update tool
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh # Download the latest stable Rust
sudo apt install -y libgtk-3-dev libasound2-dev # Latest is optional
```

#### Fedora / CentOS / Rocky Linux
```shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh # Download the latest stable Rust
sudo yum install gtk3-devel glib2-devel alsa-lib-devel # Latest is optional
```

#### macOS

Vous devez installer Rust via les bibliothèques Homebrew et GTK
```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install rustup
rustup-init
brew install rust gtk+3
```

### Les fenêtres

*Sera disponible à l'avenir*

Pour les instructions croisées de Linux à Windows, regardez le CI.

<!-- First you need to install Visual C++ components from Visual Studio installer - https://visualstudio.microsoft.com/downloads/
Next install Rust from site https://rustup.rs/
After that the latest GTK 3 runtime must be installed from https://github.com/tschoonj/GTK-for-Windows-Runtime-Environment-Installer/releases
-->

## Compilation

- Télécharger la source
```
git clone https://github.com/qarmin/czkawka.git
cd czkawka
```
- Compiler et exécuter l'interface graphique GTK
```
cargo run --release --bin czkawka_gui
```

- Compilez et exécutez la CLI (par défaut, cela imprimera l'aide avec des exemples)
```
cargo run --release --bin czkawka_cli
```


## Caractéristiques supplémentaires
Pour l'instant, la recherche de fichiers audio endommagés est temporairement désactivée par défaut, car elle se bloque lorsque les bibliothèques audio ne sont pas trouvées sur l'ordinateur. J'attends la possibilité de désactiver la fonction de lecture audio, donc après cela, je pourrai réactiver par défaut cette fonctionnalité (https://github.com/RustAudio/rodio/issues/349)

Pour activer la vérification des fichiers audio cassés, ajoutez simplement ` --all-features`
```
cargo run --all-features --bin czkawka_cli -- broken  -d /home/rafal/ -f "results.txt"
```
