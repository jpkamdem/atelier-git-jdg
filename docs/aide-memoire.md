# Aide-mémoire Git, GitHub & Codespaces

[⬅️ Retour au sommaire](../README.md)

## Les commandes de l'atelier

| Commande | À quoi ça sert | Niveau |
| --- | --- | --- |
| `git status` | Voir l'état des fichiers (modifiés, prêts, à jour…) | 1 |
| `git add <fichier>` | Préparer un fichier pour le prochain commit | 1 |
| `git commit -m "message"` | Enregistrer une version (dans le Codespace) | 1 |
| `git log --oneline --graph --all` | Voir l'historique sous forme de graphe | 1 |
| `git diff` | Voir les modifications pas encore préparées | 1 |
| `git push` | Envoyer ses commits sur GitHub | 1 |
| `git pull` | Récupérer et fusionner les commits de GitHub | 1 |
| `git switch -c <branche>` | Créer une branche et basculer dessus | 2 |
| `git switch <branche>` | Changer de branche | 2 |
| `git push -u origin <branche>` | Publier une nouvelle branche sur GitHub | 2 |
| `git merge <branche>` | Fusionner une branche dans la branche courante | 2 |
| `git fetch` | Récupérer les nouveautés de GitHub **sans** fusionner | 3 |
| `git revert <hash>` | Créer un commit qui annule un commit | 3 |
| `git stash` / `git stash pop` | Mettre de côté / récupérer des modifications | 4 |
| `git rebase -i HEAD~3` | Réécrire (regrouper, renommer) les 3 derniers commits | 4 |
| `git cherry-pick <hash>` | Copier un commit d'une autre branche | 4 |
| `git tag -a v1.0.0 -m "..."` | Marquer une version | 4 |

## Vocabulaire

| Mot | Définition |
| --- | --- |
| **Dépôt** (repository) | Un projet suivi par Git, avec tout son historique |
| **Commit** | Une version enregistrée du projet, avec un auteur, une date et un message |
| **Branche** | Une ligne de travail parallèle ; `master` est la branche principale |
| **Remote / `origin`** | Le dépôt distant (sur GitHub) relié à votre copie |
| **Clone** | Une copie complète d'un dépôt ; chaque Codespace en contient un |
| **Conflit** | Deux modifications des mêmes lignes que Git ne sait pas fusionner seul |
| **Pull Request (PR)** | Sur GitHub : une demande de fusion d'une branche, avec relecture |
| **Review** | La relecture d'une PR par un autre membre |
| **Issue** | Sur GitHub : une tâche, un bug ou une idée à traiter |
| **CI** | Des vérifications lancées automatiquement par GitHub Actions |
| **Codespace** | Une machine de développement dans le cloud, avec VS Code dans le navigateur |
| **Dev container** | La description (`.devcontainer/`) de l'environnement d'un Codespace |

## Problèmes fréquents

**`git push` refusé : `rejected ... (fetch first)`**
Quelqu'un a pushé avant vous. Faites `git pull`, résolvez les éventuels conflits, puis `git push`.

**`git push` refusé sur `master` après le niveau 3**
`master` est protégée. Déplacez votre travail sur une branche :
```bash
git switch -c ma-branche          # Vos commits partent avec vous sur la nouvelle branche
git push -u origin ma-branche
git switch master
git reset --hard origin/master    # Remet votre master au même état que GitHub
```

**Un onglet s'ouvre tout seul après `git pull`, `git merge` ou `git rebase -i`**
Git vous demande de valider un message. Modifiez-le si besoin, enregistrez (`Ctrl+S`) et **fermez l'onglet**.

**Je ne vois pas la branche de mon collègue**
Faites `git fetch`, puis `git switch <nom-de-la-branche>`.

**Il reste des `<<<<<<<` dans mon fichier**
Le conflit n'est pas résolu. Éditez le fichier, supprimez **tous** les marqueurs (`<<<<<<<`, `=======`, `>>>>>>>`), puis `git add` et `git commit`.

**J'ai fait une bêtise et je veux tout annuler (avant commit)**
`git restore .` remet tous les fichiers dans l'état du dernier commit. ⚠️ Les modifications non commitées sont perdues.

**Mon Codespace a disparu**
Les Codespaces inactifs sont arrêtés après 30 minutes et supprimés après 30 jours. Si vous aviez pushé, rien n'est perdu : créez-en un nouveau depuis le bouton **Code**.

**Je n'ai plus d'heures de Codespaces**
Vérifiez votre quota dans 🌐 **Settings → Billing and plans**. Arrêtez les Codespaces inutilisés. Le [GitHub Student Developer Pack](https://education.github.com/pack) augmente le quota gratuit.
