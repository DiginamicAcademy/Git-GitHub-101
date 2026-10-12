[← Chapitre précédent](06-Collaborer-avec-les-pull-requests.md) · [Sommaire](Readme.md)

# Aide-mémoire

Les commandes vues dans le cours, regroupées par usage.

## Configuration

| Commande | Effet |
|---|---|
| `git config --global user.name "Prénom Nom"` | nom inscrit dans les commits |
| `git config --global user.email "adresse"` | e-mail inscrit dans les commits |
| `git config --global init.defaultBranch main` | nom de la branche initiale des nouveaux dépôts |
| `git config --global pull.rebase false` | `git pull` fusionne en cas de divergence |
| `git config --global core.editor "code --wait"` | éditeur utilisé par Git |
| `git config --list --show-origin` | réglages et fichier d'origine |

## Dépôt et commits

| Commande | Effet |
|---|---|
| `git init` | créer un dépôt dans le dossier courant |
| `git status` | état du répertoire de travail et de l'index |
| `git add <fichier>` / `git add .` | indexer un fichier / tout le dossier |
| `git commit -m "message"` | enregistrer l'index dans un commit |
| `git commit -am "message"` | indexer les fichiers suivis et committer |
| `git diff` / `git diff --staged` | différences non indexées / indexées |
| `git log --oneline --graph --all` | historique compact, avec les branches |
| `git show <hash>` | détail d'un commit |

## Annuler

| Commande | Effet |
|---|---|
| `git restore <fichier>` | abandonner les modifications non indexées (perdues) |
| `git restore --staged <fichier>` | retirer de l'index, garder les modifications |
| `git commit --amend` | corriger le dernier commit, s'il n'est pas partagé |
| `git revert <hash>` | annuler un commit partagé par un nouveau commit |
| `git rm --cached <fichier>` | arrêter de suivre un fichier sans le supprimer |

## Branches

| Commande | Effet |
|---|---|
| `git branch` | lister les branches |
| `git switch -c <branche>` | créer une branche et basculer dessus |
| `git switch <branche>` | changer de branche |
| `git merge <branche>` | fusionner une branche dans la branche courante |
| `git merge --abort` | abandonner une fusion en conflit |
| `git branch -d <branche>` | supprimer une branche fusionnée (`-D` pour forcer) |

## Dépôts distants

| Commande | Effet |
|---|---|
| `git clone <url>` | copier un dépôt distant |
| `git remote add origin <url>` | déclarer un dépôt distant |
| `git remote -v` | lister les dépôts distants |
| `git push -u origin <branche>` | premier envoi d'une branche, avec suivi |
| `git push` / `git pull` | envoyer / récupérer et fusionner |
| `git fetch` | récupérer sans fusionner |

## GitHub CLI

| Commande | Effet |
|---|---|
| `gh auth login` / `gh auth status` | se connecter / vérifier la connexion |
| `gh repo create <dépôt> --private --source=. --push` | publier le dépôt local courant |
| `gh repo fork <compte>/<dépôt> --clone` | forker et cloner |
| `gh pr create --fill` | ouvrir une pull request |
| `gh pr list` / `gh pr checkout <n>` | lister les PR / récupérer une PR en local |

## Références

- Documentation de Git : [git-scm.com/docs](https://git-scm.com/docs)
- Livre Pro Git, en français : [git-scm.com/book/fr/v2](https://git-scm.com/book/fr/v2)
- Documentation de GitHub : [docs.github.com/fr](https://docs.github.com/fr)
- Manuel de la GitHub CLI : [cli.github.com/manual](https://cli.github.com/manual/)
- Modèles de `.gitignore` : [github.com/github/gitignore](https://github.com/github/gitignore)
- Changements prévus pour Git 3.0 : [git-scm.com/docs/BreakingChanges](https://git-scm.com/docs/BreakingChanges)

---

[← Chapitre précédent](06-Collaborer-avec-les-pull-requests.md) · [Sommaire](Readme.md)
