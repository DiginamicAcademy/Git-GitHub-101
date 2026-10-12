[← Chapitre précédent](01-Pourquoi-Git.md) · [Sommaire](Readme.md) · [Chapitre suivant →](03-Premiers-commits.md)

# Installer et configurer Git

## 🎯 Objectifs

À la fin de ce chapitre, vous aurez :

1. Installé une version récente de Git.
2. Configuré votre identité, la branche par défaut et votre éditeur.
3. Vérifié l'installation.

> Les procédures ci-dessous suivent la documentation officielle à la date du 7 octobre 2026. En cas de doute, c'est elle qui fait foi : [git-scm.com/install](https://git-scm.com/install/).

---

## 1. Installer Git

Vérifiez d'abord si Git est déjà présent, et dans quelle version :

```bash
git --version
```

Si la commande répond avec une version récente (2.5x ou plus), passez à la section 2.

### Windows : Git for Windows

Deux possibilités :

- l'installeur, à télécharger depuis [git-scm.com/install/windows](https://git-scm.com/install/windows) ;
- `winget`, dans un terminal PowerShell :

```powershell
winget install --id Git.Git -e --source winget
```

Git for Windows fournit Git, **Git Bash** (un terminal bash pour Windows) et **Git Credential Manager**, qui mémorise vos identifiants GitHub de façon sécurisée. Les options par défaut de l'installeur conviennent ; deux écrans méritent un coup d'œil :

- **éditeur par défaut** : choisissez celui que vous utilisez (Visual Studio Code, Notepad++…) plutôt que Vim si vous ne le connaissez pas ;
- **nom de la branche initiale** : choisissez « Override the default branch name for new repositories » avec `main`.

Fermez puis rouvrez votre terminal après l'installation.

### macOS

- Taper `git --version` dans le Terminal propose d'installer les **Command Line Tools** d'Apple, qui contiennent Git. C'est suffisant pour ce cours, mais la version d'Apple a souvent quelques mois de retard.
- Pour une version à jour, utilisez [Homebrew](https://brew.sh/) :

```bash
brew install git      # première installation
brew upgrade git      # mise à jour
```

### Linux (Ubuntu / Debian)

```bash
sudo apt update
sudo apt install git
```

La version des dépôts de la distribution peut dater un peu. Sur Ubuntu, le PPA officiel des mainteneurs de Git fournit la dernière version stable :

```bash
sudo add-apt-repository ppa:git-core/ppa
sudo apt update
sudo apt install git
```

Pour Fedora : `sudo dnf install git`. Autres distributions : [git-scm.com/install/linux](https://git-scm.com/install/linux).

---

## 2. Configurer Git

La configuration se fait une fois par machine, avec `git config --global`. Elle est enregistrée dans le fichier `~/.gitconfig`.

### Votre identité

Chaque commit enregistre un nom et une adresse e-mail. Utilisez l'adresse associée à votre compte GitHub (ou l'adresse `noreply` que GitHub vous attribue, si vous ne voulez pas publier votre e-mail) :

```bash
git config --global user.name "Prénom Nom"
git config --global user.email "prenom.nom@example.com"
```

### La branche par défaut

Git nomme encore `master` la première branche d'un nouveau dépôt ; GitHub et les autres plateformes utilisent `main`, et Git 3.0 fera de même. Alignez-vous dès maintenant :

```bash
git config --global init.defaultBranch main
```

### Le comportement de `git pull`

Quand votre branche locale et la branche distante ont toutes deux avancé, Git refuse de choisir à votre place comment les réunir. Indiquez-lui de **fusionner** (le comportement historique, le plus simple à comprendre au départ) :

```bash
git config --global pull.rebase false
```

### Votre éditeur

Git ouvre un éditeur pour certains messages (commit sans `-m`, fusion…). Exemple avec Visual Studio Code :

```bash
git config --global core.editor "code --wait"
```

### Les fins de ligne

Windows termine les lignes par `CRLF`, macOS et Linux par `LF`. Pour éviter les fichiers « modifiés » sans raison dans une équipe mixte, la règle la plus robuste se place **dans le dépôt**, avec un fichier `.gitattributes` :

```text
* text=auto
```

Git normalise alors les fichiers texte en `LF` dans l'historique. Sous Windows, l'installeur règle en plus `core.autocrlf=true`, qui convertit en `CRLF` dans la copie de travail : gardez ce réglage.

---

## 3. Vérifier

```bash
git --version
git config --global --list
```

La seconde commande affiche les réglages enregistrés. Pour savoir **d'où** vient chaque réglage (système, utilisateur, dépôt) :

```bash
git config --list --show-origin
```

---

## 4. À vous de jouer

Installez Git, appliquez les réglages de la section 2, puis vérifiez-les.

<details>
<summary>Voir le résultat attendu</summary>

```bash
git --version
# git version 2.56.0   (ou plus récent ; sous Windows, un suffixe s'ajoute : 2.56.0.windows.2)

git config --global --list
# user.name=Prénom Nom
# user.email=prenom.nom@example.com
# init.defaultbranch=main
# pull.rebase=false
# core.editor=code --wait
```

Git affiche les noms de réglages en minuscules (`init.defaultbranch`) : c'est normal, ils ne sont pas sensibles à la casse. Les réglages posés par l'installeur de Git for Windows (`credential.helper`, `core.autocrlf`…) sont au niveau **système** : ils n'apparaissent qu'avec `git config --list --show-origin`.

</details>

---

[← Chapitre précédent](01-Pourquoi-Git.md) · [Sommaire](Readme.md) · [Chapitre suivant →](03-Premiers-commits.md)
