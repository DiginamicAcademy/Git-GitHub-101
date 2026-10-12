<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/Logo-diginamic-color-blk.png">
    <img src="assets/Logo-diginamic-color.svg" alt="Diginamic Formation" width="358">
  </picture>
</p>

# Git et GitHub 101

Un cours pour (re)voir les bases de Git et de GitHub, pas à pas : installer et configurer Git, versionner son travail, utiliser les branches, publier sur GitHub et collaborer par pull request.

## 🎯 Objectifs pédagogiques

À la fin de ce cours, vous saurez :

1. Expliquer ce qu'est un gestionnaire de versions distribué, et la différence entre Git et GitHub.
2. Installer et configurer Git sur Windows, macOS ou Linux.
3. Créer un dépôt, enregistrer des modifications en commits et consulter l'historique.
4. Créer des branches, les fusionner et résoudre un conflit.
5. Relier un dépôt local à GitHub, pousser, récupérer et cloner.
6. Proposer une modification par pull request et la faire relire.

## ❔ Pourquoi ce cours ?

Git est l'outil de gestion de versions de référence, et GitHub la principale plateforme d'hébergement et de collaboration autour de Git. Presque tout projet logiciel, mais aussi beaucoup de documentation et de supports de cours, passe par eux. Les autres cours (Docker, CI/CD, développement…) supposent ce socle acquis. Ce cours le pose, ou le remet à plat.

## Prérequis

- Être à l'aise avec un terminal (bash, zsh ou PowerShell).
- Un éditeur de texte (Visual Studio Code ou autre).
- Les droits nécessaires pour installer un logiciel sur sa machine.
- Une adresse e-mail pour créer un compte GitHub gratuit.

## Le parcours

Chaque étape est un fichier. On les suit **dans l'ordre** : chacune s'appuie sur la base laissée par la précédente.

| # | Étape | Ce qu'on y fait |
|---|---|---|
| [01](01-Pourquoi-Git.md) | Pourquoi Git ? | gestion de versions, modèle distribué, vocabulaire, Git vs GitHub |
| [02](02-Installer-et-configurer-Git.md) | Installer et configurer Git | installation (Windows, macOS, Linux), identité, branche par défaut, vérification |
| [03](03-Premiers-commits.md) | Premiers commits | les trois zones, `init`, `status`, `add`, `commit`, `log`, `diff`, `.gitignore`, annuler |
| [04](04-Branches-et-fusions.md) | Branches et fusions | `branch`, `switch`, `merge`, résolution de conflit |
| [05](05-Travailler-avec-GitHub.md) | Travailler avec GitHub | compte, authentification, `remote`, `push`, `pull`, `clone`, GitHub CLI |
| [06](06-Collaborer-avec-les-pull-requests.md) | Collaborer avec les pull requests | GitHub Flow, pull request, relecture, fusion, fork |
| [A](A-Aide-memoire.md) | Aide-mémoire | les commandes du cours sur une page, liens de référence |

## Versions de référence

Vérifiées le 7 octobre 2026. Git et GitHub évoluent souvent : les commandes du cours restent valables, seuls les numéros changent.

| Composant | Version de référence |
|---|---|
| Git | 2.56 |
| Git for Windows | 2.56 |
| GitHub CLI (`gh`) | 2.x |

> **Git 3.0 est annoncé** mais n'a pas de date de sortie à ce jour. Parmi ses changements : la branche par défaut des nouveaux dépôts deviendra `main` (le cours la configure dès maintenant) et l'empreinte des objets passera de SHA-1 à SHA-256. Les commandes de ce cours ne changent pas.
