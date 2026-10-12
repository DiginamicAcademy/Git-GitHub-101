---
marp: true
theme: default
style: |
  section {background-color: #121114}
  h1,h2,h3 {color: #8393f0}
  p,ul,li,td,th {color: #ccc}
  section table {font-size: 0.85em}
  section table td {background-color: #121114}
  section table th {background-color: #272133; font-weight: bolder}
  pre {background-color: #17151a; color: #ccc}
  blockquote {border: 2px green solid; border-left-width: 15px; padding: 0.5em 15px;font-style: italic }
paginate: true
header: "Git et GitHub 101"
footer: "![height:20px](https://raw.githubusercontent.com/DiginamicInternal/PublicAssets/refs/heads/main/Logo-diginamic-color-blk.png)"
---

# Git et GitHub 101

### Versionner, partager, collaborer : les bases, pas à pas

<!-- Vérifier en début de séance que chacun a un compte GitHub, ou le faire créer pendant le chapitre 02. -->

---

## 🎯 Objectifs pédagogiques

À la fin de ce cours, vous saurez :

1. Expliquer la gestion de versions distribuée, et Git vs GitHub
2. Installer et configurer Git
3. Enregistrer des commits et consulter l'historique
4. Créer des branches, fusionner, résoudre un conflit
5. Publier et synchroniser un dépôt sur GitHub
6. Proposer une modification par pull request

---

## Le parcours

| #  | Étape                               |
|----|-------------------------------------|
| 01 | Pourquoi Git ?                      |
| 02 | Installer et configurer Git         |
| 03 | Premiers commits                    |
| 04 | Branches et fusions                 |
| 05 | Travailler avec GitHub              |
| 06 | Collaborer avec les pull requests   |

Chaque étape s'appuie sur la précédente : on les suit **dans l'ordre**.

---

# 1. Pourquoi Git ?

---

## `rapport-final-v3-VRAIMENT-final.docx`

Un gestionnaire de versions :

- enregistre l'historique complet, en **instantanés** commentés
- permet de revenir à n'importe quel état passé
- montre **quoi**, **quand** et **qui**
- permet de travailler à plusieurs **en parallèle**

Pas seulement pour le code : documentation, configuration, supports en Markdown…

---

## Un modèle distribué

```text
        Dépôt sur GitHub (référence commune)
          ▲  │                    ▲  │
     push │  │ pull          push │  │ pull
          │  ▼                    │  ▼
  Dépôt local d'Alice      Dépôt local de Bob
```

- Chaque copie contient **tout l'historique**
- On travaille hors ligne, on synchronise quand on veut

---

## Le vocabulaire

| Terme | En une phrase |
|---|---|
| **Dépôt** | les fichiers + tout l'historique (dossier `.git`) |
| **Commit** | un instantané, avec auteur, date, message et hash |
| **Branche** | une ligne de développement : un pointeur vers un commit |
| **`HEAD`** | là où l'on travaille actuellement |
| **Remote** | une autre copie du dépôt, `origin` par convention |
| **Merge** | réunir le travail de deux branches |
| **Pull request** | une demande de fusion, avec relecture, sur GitHub |

---

## Git n'est pas GitHub

| | Git | GitHub |
|---|---|---|
| Nature | logiciel libre, sur votre machine | service en ligne |
| Rôle | versionner | héberger et collaborer |
| Sans l'autre ? | oui, entièrement en local | non |
| En plus | — | PR, issues, Actions, Pages… |

Alternatives à GitHub : GitLab, Bitbucket, Gitea, Forgejo. Les commandes Git restent les mêmes.

---

# 2. Installer et configurer Git

---

## Installer

```text
winget install --id Git.Git -e --source winget   # Windows
brew install git                                 # macOS
sudo apt install git                             # Ubuntu / Debian
git --version                                    # 2.56 à date
```

- macOS : les Command Line Tools d'Apple suffisent aussi, mais sont souvent en retard
- Windows : Git for Windows fournit aussi **Git Bash** et **Git Credential Manager**

---

## Configurer, une fois par machine

```bash
git config --global user.name "Prénom Nom"
git config --global user.email "prenom.nom@example.com"
git config --global init.defaultBranch main
git config --global pull.rebase false
git config --global core.editor "code --wait"
```

Vérifier : `git config --list --show-origin`

> `main` deviendra la branche par défaut avec Git 3.0 : autant s'aligner dès maintenant.

---

# 3. Premiers commits

---

## Les trois zones

```text
Répertoire de travail ──git add──▶ Index ──git commit──▶ Dépôt (.git)
        ▲                                                    │
        └──────────────────── git restore ───────────────────┘
```

L'**index** prépare le prochain commit : on choisit ce qu'on y met.

---

## Le cycle de base

```bash
git init
git status                 # que se passe-t-il ?
git add README.md          # indexer
git commit -m "Ajoute le README"
git diff                   # modifications non indexées
git diff --staged          # modifications indexées
git log --oneline --graph --all
```

> Toujours un `git status` avant de committer.

---

## Bons messages, bon `.gitignore`

**Message de commit** : une première ligne courte qui dit ce que fait le commit (« Corrige le calcul de la TVA »), puis le pourquoi si besoin.

```text
node_modules/
dist/
*.log
# Les secrets ne se versionnent jamais
.env
```

Un fichier déjà suivi n'est pas ignoré : `git rm --cached <fichier>`.

---

## Annuler

| Situation | Commande |
|---|---|
| Abandonner une modification non indexée | `git restore <fichier>` |
| Désindexer | `git restore --staged <fichier>` |
| Corriger le dernier commit, non partagé | `git commit --amend` |
| Annuler un commit partagé | `git revert <hash>` |

> ⚠️ `git restore <fichier>` est définitif. `git revert` ne détruit rien.

---

## Exercice

1. Créer un dépôt `exo-git` avec `notes.md` (« Première ligne »), committer
2. Ajouter une ligne, observer `git diff`, committer
3. Faire ignorer un fichier `secret.env`, committer le `.gitignore`
4. Ajouter une ligne puis l'annuler sans committer
5. Combien de commits dans `git log --oneline` ?

---

# 4. Branches et fusions

---

## Branches

```bash
git branch                   # lister
git switch -c page-contact   # créer et basculer
git switch main              # revenir
git merge page-contact       # fusionner dans la branche courante
git branch -d page-contact   # supprimer une branche fusionnée
```

- Une branche = un **pointeur** : la créer est instantané
- Une branche par fonctionnalité ou correction ; `main` reste stable

---

## Deux façons de fusionner

| Cas | Résultat |
|---|---|
| `main` n'a pas bougé | **fast-forward** : `main` avance simplement |
| `main` a avancé aussi | **commit de fusion**, à deux parents |

```text
* Merge branch 'titre-anglais'
|\
| * Traduit le titre
* | Renomme le titre
|/
* Ajoute un titre aux notes
```

---

## Les conflits

```text
<<<<<<< HEAD
<h1>Bienvenue sur mon site</h1>
=======
<h1>Bienvenue !</h1>
>>>>>>> titre-court
```

1. Éditer : garder la bonne version, **supprimer les marqueurs**
2. `git add <fichier>`
3. `git commit`

`git merge --abort` pour tout annuler. Un conflit n'est pas une erreur : Git vous demande de trancher.

---

## Exercice

1. Branche `ajout-titre` : ajouter `# Mes notes` en tête, committer
2. Fusionner dans `main` : quel type de fusion ?
3. Branche `titre-anglais` : titre `# My notes`, committer
4. Sur `main` : titre `# Notes de cours`, committer
5. Fusionner `titre-anglais`, résoudre en gardant `# Notes de cours`
6. `git log --oneline --graph --all`, puis supprimer les branches

---

# 5. Travailler avec GitHub

---

## S'authentifier

GitHub **refuse le mot de passe** pour `push` et `pull`.

| Accès | Mise en place |
|---|---|
| **HTTPS** (recommandé) | `gh auth login`, ou Git Credential Manager (Windows) |
| **SSH** | `ssh-keygen -t ed25519`, clé publique déclarée sur GitHub |

```bash
winget install --id GitHub.cli   # ou : brew install gh
gh auth login                    # GitHub.com → HTTPS → navigateur
gh auth status
```

Activer l'**authentification à deux facteurs** sur le compte GitHub.

---

## Publier un dépôt local

Interface web : **New repository**, sans README ni `.gitignore`, puis :

```bash
git remote add origin https://github.com/<compte>/<dépôt>.git
git push -u origin main
```

Ou, en une commande :

```bash
gh repo create <dépôt> --private --source=. --push
```

---

## Synchroniser

| Commande | Effet |
|---|---|
| `git push` | envoyer ses commits |
| `git fetch` | récupérer, sans toucher à son travail |
| `git pull` | `fetch` + fusion |
| `git clone <url>` | copie complète, `origin` configuré |

> Push refusé ? `git pull`, résoudre, puis `git push`.
> Prendre l'habitude du `git pull` avant de commencer à travailler.

---

## Exercice

1. Publier `exo-git` sur GitHub, en **privé**
2. Modifier `notes.md` directement sur GitHub
3. En local : `git status` voit-il la modification ? La récupérer
4. Cloner le dépôt dans un autre dossier et vérifier l'historique

---

# 6. Collaborer avec les pull requests

---

## Le GitHub Flow

```text
main à jour ─▶ branche ─▶ commits + push ─▶ pull request
     ▲                                          │
     └── suppression de la branche ◀── fusion ◀─┘  relecture
```

```bash
git switch main && git pull
git switch -c corrige-coquilles
git commit -am "Corrige les coquilles du README"
git push -u origin corrige-coquilles
gh pr create --fill
```

`Closes #12` dans la description ferme le ticket 12 à la fusion.

---

## Relire et fusionner

**Revue** : *Comment*, *Approve* ou *Request changes*. Les corrections se poussent sur la même branche.

| Méthode de fusion | Dans `main` |
|---|---|
| Merge commit | tous les commits + un commit de fusion |
| **Squash and merge** | un seul commit pour la PR |
| Rebase and merge | les commits, sans commit de fusion |

```bash
git switch main && git pull && git branch -d corrige-coquilles
```

---

## Le fork

Pas de droits d'écriture ? On **forke** : copie sous son compte, push dans le fork, PR vers l'origine.

```bash
gh repo fork <compte>/<dépôt> --clone
```

| | Branche | Fork |
|---|---|---|
| Droits | écriture sur le dépôt | aucun (dépôt public) |
| Cas typique | équipe d'un projet | open source, contributeur externe |

---

## Exercice

1. Créer un ticket « Ajouter une section Sources »
2. Branche + section `## Sources` dans `notes.md`, push
3. Pull request avec `Closes #<n>` dans la description
4. Commenter une ligne, pousser une correction
5. **Squash and merge**, supprimer la branche, `git pull`
6. Le ticket est-il fermé ? Combien de commits pour la PR ?

---

## Pour aller plus loin

- `git rebase` : historique linéaire, sur ses propres branches
- `git stash` : mettre de côté des modifications
- GitHub Actions : tests et déploiements automatiques
- Pro Git, en français : [git-scm.com/book/fr/v2](https://git-scm.com/book/fr/v2)

---

# Des questions ?

### L'aide-mémoire est en annexe du support

Pour toute question [adressez-vous au service pédagogie](mailto:pedagogie@diginamic.fr)
