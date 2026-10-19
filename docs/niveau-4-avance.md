# Niveau 4 — Pratiques avancées

⬅️ [Niveau 3](niveau-3-workflow-github.md) · [Sommaire](../README.md)

**Durée indicative :** 2 h · **20 points**

## Objectifs

- Comprendre que l'environnement Codespace est lui aussi **versionné**.
- Mettre du travail de côté (`stash`), nettoyer son historique (`rebase -i`), récupérer un commit précis (`cherry-pick`).
- Automatiser des vérifications avec **GitHub Actions**.
- Publier une version avec un **tag** et une **release**.

> Toutes les règles du niveau 3 restent valables : **une branche + une PR relue** pour chaque changement.

---

## Exercice 4.1 — Le Codespace, c'est du code (2 pts) — collab-3

Pourquoi tous vos Codespaces ont-ils les mêmes extensions (Live Preview, Git Graph…) ? Parce qu'elles sont décrites dans le fichier `.devcontainer/devcontainer.json` du dépôt.

1. 💻 Ouvrez `.devcontainer/devcontainer.json` et lisez-le.
2. Sur une branche `chore/devcontainer`, ajoutez l'extension **HTMLHint** à la liste `extensions` :
   ```json
   "HTMLHint.vscode-htmlhint"
   ```
3. PR, review, fusion.
4. **Tout le monde** : `git switch master && git pull`, puis appliquez la nouvelle configuration :
   `F1` (ou `Ctrl+Shift+P`) → **Codespaces: Rebuild Container**.
5. Après le redémarrage, ouvrez `index.html` : les erreurs HTML sont soulignées directement dans l'éditeur.

> Ce que ça montre : l'environnement de travail est **dans le dépôt**, comme le code. Un nouveau membre qui ouvre un Codespace a exactement les mêmes outils que vous, sans rien installer.
> Vos fichiers sont conservés pendant le *Rebuild*, mais pensez à commiter avant par sécurité.

---

## Exercice 4.2 — `git stash` : mettre son travail de côté (3 pts) — tout le monde

Scénario : vous êtes en plein travail, et une urgence tombe.

💻 **Codespace**

1. Sur `master` à jour, modifiez n'importe quel fichier **sans commiter**.
2. Urgence ! Mettez votre travail en cours de côté :
   ```bash
   git stash
   git status              # Plus aucune modification : elles sont rangées
   git stash list          # Elles sont ici
   ```
3. Traitez l'urgence : créez une branche `fix/urgence-<prenom>`, ajoutez à votre fiche `equipe/<prenom>.md` une section `## Stash` qui explique en 3 lignes à quoi sert `git stash`. Commit, push, PR.
4. Revenez à votre travail :
   ```bash
   git switch master
   git stash pop           # Vos modifications reviennent
   ```
5. Annulez ensuite ces modifications de test : `git restore .`

---

## Exercice 4.3 — `git rebase -i` : un historique propre (5 pts)

En vrai, on commite souvent des étapes intermédiaires (`wip`, `oups`, `fix typo`). Avant de les partager, on peut les **regrouper** en un seul commit propre.

### Les missions

| Membre | Branche | Mission |
| --- | --- | --- |
| collab-1 | `feature/responsive` | Ajouter dans `style.css` une règle `@media (max-width: 600px)` qui réduit la taille des titres. |
| collab-2 | `feature/dark-mode` | Ajouter une classe `.dark` (fond noir, texte blanc) et l'appliquer au `<body>`. |
| collab-3 | `feature/nav` | Ajouter un `<nav>` avec des liens vers `index.html`, `contact.html` et `cours.html` sur les 3 pages. |

### La procédure

1. Faites **au moins 3 commits** sur votre branche, dont 2 « brouillons » :
   ```bash
   git commit -am "wip"
   git commit -am "oups"
   git commit -am "feat(style): ajoute le mode sombre"
   ```
2. **Avant de pusher**, regroupez les 3 derniers commits :
   ```bash
   git rebase -i HEAD~3
   ```
3. Un onglet s'ouvre dans VS Code avec la liste des commits (du plus ancien au plus récent) :
   ```
   pick a1b2c3d wip
   pick d4e5f6a oups
   pick 7a8b9c0 feat(style): ajoute le mode sombre
   ```
   Remplacez `pick` par `squash` (ou `s`) sur les **2 dernières** lignes. Enregistrez (`Ctrl+S`) et **fermez l'onglet**.
4. Un deuxième onglet s'ouvre pour le message du commit final. Ne gardez qu'un message propre, enregistrez, fermez l'onglet.
5. Vérifiez : `git log --oneline` n'affiche plus qu'**un** commit pour votre mission.
6. `git push -u origin <branche>`, puis PR, review, fusion.

> Si vous aviez **déjà pushé** la branche avant le rebase, Git refusera le push. Utilisez alors :
> `git push --force-with-lease`
> Il écrase votre branche sur GitHub, mais refuse si quelqu'un d'autre y a pushé entre-temps.
>
> ⛔ **Jamais de force-push sur `master`**, ni sur une branche sur laquelle d'autres travaillent.

---

## Exercice 4.4 — `git cherry-pick` : récupérer un commit précis (3 pts)

Scénario : une branche contient 3 commits, mais seuls 2 vous intéressent.

1. **collab-1** crée une branche `improvements` depuis `master`, avec 3 commits **séparés** :
   - **A** : ajoute dans le `<head>` de `index.html` une balise `<meta name="description" content="Site de l'école">` ;
   - **B** : ajoute `<meta name="viewport" content="width=device-width, initial-scale=1">` ;
   - **C** : ajoute une bannière publicitaire bien moche (fond jaune fluo, texte clignotant…).

   Il pushe la branche **sans ouvrir de PR**.

2. **collab-2** récupère seulement A et B :
   ```bash
   git fetch
   git log --oneline origin/improvements     # Notez les hash de A et B
   git switch master && git pull
   git switch -c feature/meta
   git cherry-pick <hashA> <hashB>
   git push -u origin feature/meta
   ```
3. PR, review, fusion. La branche `improvements` peut ensuite être supprimée.

> `cherry-pick` copie un commit d'une autre branche sur la vôtre. Pratique pour récupérer un correctif sans tout le reste.

---

## Exercice 4.5 — GitHub Actions : une vérification automatique (4 pts)

Une **CI** (intégration continue) est un script que GitHub exécute automatiquement, sur ses propres machines, à chaque push ou PR.

### D'abord, à la main dans le Codespace 💻

```bash
npx --yes htmlhint *.html
```

Si des erreurs apparaissent, corrigez-les. C'est **exactement** cette commande que la CI va lancer.

### Ensuite, automatiquement sur GitHub 🌐

1. Sur une branche `chore/ci`, créez le fichier `.github/workflows/lint.yml` :
   ```yaml
   name: Lint HTML

   on:
     pull_request:
       branches: [master]
     push:
       branches: [master]

   jobs:
     lint:
       runs-on: ubuntu-latest
       steps:
         - name: Récupérer le code
           uses: actions/checkout@v4

         - name: Vérifier que les pages existent
           run: |
             test -f index.html
             test -f contact.html
             test -f cours.html

         - name: Vérifier le HTML
           run: npx --yes htmlhint *.html
   ```
2. Pushez et ouvrez la PR : en bas de la PR, la vérification **Lint HTML** se lance. Attendez qu'elle soit ✅ verte, puis fusionnez.
3. **Cassez-la volontairement** : sur une nouvelle branche, supprimez une balise fermante (par exemple `</section>`) et ouvrez une PR. La CI passe en ❌ rouge.
   Cliquez sur **Details** pour lire l'erreur.
4. **Réparez** sur la même branche, pushez : la CI repasse au vert. Fusionnez.

> Mettez dans la description de cette dernière PR **le lien vers un run rouge et vers un run vert** (onglet **Actions** du dépôt).
>
> 💡 Pour aller plus loin : dans la règle de protection de `master`, ajoutez **Require status checks to pass** → `lint`. Une PR rouge ne pourra plus être fusionnée.

---

## Exercice 4.6 — Tags et releases (3 pts) — collab-1

Il est temps de publier la **v1.0.0** !

1. 💻 Sur `master` à jour :
   ```bash
   git tag -a v1.0.0 -m "Première version stable du site"
   git push origin v1.0.0
   ```
2. 🌐 Sur GitHub : **Releases** → **Draft a new release** → choisissez le tag `v1.0.0`.
3. Rédigez les notes de version :
   ```markdown
   ## Nouveautés
   - Pages Contact et Cours
   - Navigation, mode sombre, affichage mobile

   ## Corrections
   - Fautes d'orthographe

   ## Technique
   - Vérification automatique du HTML (GitHub Actions)
   - Environnement Codespace configuré
   ```
   (Le bouton **Generate release notes** peut vous proposer une liste à partir des PR.)
4. **Publish release**.
5. Faites une petite correction (branche + PR), puis publiez de la même façon la **v1.0.1**.

> **Versionnage sémantique** `MAJEUR.MINEUR.CORRECTIF` :
> - `1.0.0 → 1.0.1` : correction de bug ;
> - `1.0.1 → 1.1.0` : nouvelle fonctionnalité compatible ;
> - `1.1.0 → 2.0.0` : changement qui casse la compatibilité.

---

## 🎉 Fin de l'atelier

Vérifiez la [liste de livraison](../README.md#6-livraison-finale), puis **arrêtez vos Codespaces** :
🌐 [github.com/codespaces](https://github.com/codespaces) → `...` → **Stop codespace** (ou **Delete** si tout est pushé).

Avant de supprimer, posez-vous la question du niveau 1 : *« Tout est-il bien pushé sur GitHub ? »*
`git status` doit afficher `Your branch is up to date with 'origin/master'` et `nothing to commit`.
