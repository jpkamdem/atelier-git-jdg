# Niveau 3 — Le workflow GitHub : planifier, proposer, relire

⬅️ [Niveau 2](niveau-2-branches.md) · [Sommaire](../README.md) · ➡️ [Niveau 4](niveau-4-avance.md)

**Durée indicative :** 2 h · **30 points**

## Objectifs

- Planifier le travail avec les **Issues** et un **Project**.
- Interdire les fusions directes sur `master`.
- Proposer ses changements par **Pull Request** (PR) et les faire **relire** (code review).
- Résoudre un conflit dans une PR.
- Ignorer des fichiers et annuler un commit proprement.

### Ce qui change par rapport au niveau 2

| Niveau 2 | Niveau 3 |
| --- | --- |
| On fusionne avec `git merge` dans son Codespace 💻 | On fusionne via une **Pull Request** sur GitHub 🌐 |
| Personne ne relit | Un autre membre **relit et approuve** avant la fusion |
| On se répartit le travail à l'oral | Le travail est écrit dans des **Issues** |

Git (les commits, les branches) reste le même. **GitHub ajoute la collaboration par-dessus.**

---

## Exercice 3.1 — Issues et tableau de suivi (4 pts)

🌐 **GitHub**

1. Onglet **Projects** → **New project** → modèle **Board**. Nommez-le `Atelier Git`.
   Vous avez 3 colonnes : `Todo`, `In Progress`, `Done`.
2. Onglet **Issues** → **New issue** : créez **une issue par mission** de l'exercice 3.3 (3 issues).
3. Pour chaque issue :
   - assignez-la à la personne qui la réalise (**Assignees**) ;
   - ajoutez-la au projet (**Projects** → `Atelier Git`).

Une issue **bien rédigée** contient un titre clair, le besoin, et des critères d'acceptation sous forme de cases à cocher :

```markdown
## Besoin
Les visiteurs doivent pouvoir trouver nos coordonnées.

## Critères d'acceptation
- [ ] Le fichier contact.html existe
- [ ] Il utilise style.css
- [ ] Un lien y mène depuis index.html
```

> La moitié des points porte sur la **qualité de rédaction** des issues.

Pendant tout le niveau, déplacez vos cartes de colonne en colonne au fil de votre avancement.

---

## Exercice 3.2 — Protéger `master` (2 pts)

🌐 **GitHub** — collab-1 (propriétaire) uniquement :

1. **Settings** → **Branches** → **Add branch ruleset** (ou **Add classic branch protection rule**).
2. Cible : la branche `master`.
3. Cochez **Require a pull request before merging**, avec **1 approbation** minimum.
4. Enregistrez.

Testez : faites un petit commit sur `master` dans votre Codespace et essayez `git push`. ❌ Refusé ! Annulez ce commit avec `git reset --hard origin/master`.

> À partir de maintenant, **tout** changement sur `master` passe par une PR approuvée par quelqu'un d'autre.

---

## Exercice 3.3 — Pull Requests et code review (12 pts)

### Les missions

| Membre | Branche | Mission |
| --- | --- | --- |
| collab-1 | `feature/contact` | Créer `contact.html` (titre, email et téléphone fictifs), utilisant `style.css`. Ajouter un lien vers cette page depuis `index.html`. |
| collab-2 | `feature/cours` | Créer `cours.html` avec une liste d'au moins 4 cours, utilisant `style.css`. Ajouter un lien vers cette page depuis `index.html`. |
| collab-3 | `fix/titre` | Relire tout `index.html` et corriger les fautes restantes (il en reste au moins une). |

### Le circuit d'une Pull Request

**1. L'auteur travaille dans son Codespace** 💻

```bash
git switch master && git pull
git switch -c feature/contact
# ... modifications, commits ...
git push -u origin feature/contact
```

**2. L'auteur ouvre la PR** 🌐

- Sur le dépôt, un bandeau jaune propose **Compare & pull request**. Cliquez dessus.
- Vérifiez : `base: master` ← `compare: feature/contact`.
- Titre clair, description qui explique **quoi** et **pourquoi**.
- Dans la description, écrivez `Closes #1` (le numéro de votre issue) : l'issue se fermera automatiquement à la fusion.
- À droite, **Reviewers** : choisissez un autre membre.

**3. Le relecteur relit** 🌐 + 💻

- Sur GitHub, onglet **Files changed** : lisez le code, cliquez sur le `+` à côté d'une ligne pour commenter.
- Pour **tester** la page, récupérez la branche dans **votre** Codespace :
  ```bash
  git fetch
  git switch feature/contact
  ```
  puis clic droit sur `contact.html` → **Show Preview**. Revenez ensuite sur `master` (`git switch master`).
- Terminez la review : **Review changes** → laissez **au moins un commentaire constructif** → **Approve** (ou **Request changes** s'il faut corriger).

> Une review qui dit juste « LGTM » sans commentaire = **0 point** pour cette PR.
> Un bon commentaire : « Le lien vers contact.html n'a pas de texte alternatif clair, tu pourrais écrire "Nous contacter" plutôt que "ici" ? »

**4. L'auteur corrige si besoin**

Il commite et pushe sur **la même branche** : la PR se met à jour toute seule.

**5. Fusion** 🌐

Une fois la PR approuvée : **Squash and merge** → **Confirm**. Puis **Delete branch**.

> **Squash and merge** regroupe tous les commits de la PR en un seul sur `master`. Utilisez cette option pour toutes les PR de l'atelier : l'historique de `master` reste lisible.

**6. Tout le monde se met à jour** 💻

```bash
git switch master
git pull
```

> 💡 Bonus pratique : l'extension **GitHub Pull Requests** (icône dans la barre de gauche du Codespace) permet de faire toutes ces étapes sans quitter VS Code.

✅ **Checkpoint** : les 3 PR sont fusionnées, les 3 issues sont fermées automatiquement, et les cartes sont dans `Done`.

---

## Exercice 3.4 — Un conflit dans une Pull Request (7 pts)

On crée volontairement un conflit entre deux PR.

1. **collab-1** et **collab-2** partent tous les deux d'un `master` à jour, **en même temps** :
   - collab-1 crée `feature/footer-1` et ajoute juste avant `</body>` dans `index.html` :
     ```html
     <footer>© 2026 ESGI — Tous droits réservés</footer>
     ```
   - collab-2 crée `feature/footer-2` et ajoute **au même endroit** :
     ```html
     <footer>Site réalisé dans le cadre de l'atelier Git</footer>
     ```
2. Chacun pushe et ouvre sa PR.
3. La PR de **collab-1** est relue et fusionnée en premier.
4. Sur la PR de **collab-2**, GitHub affiche : *This branch has conflicts that must be resolved*.

**collab-2 résout le conflit dans son Codespace** 💻 :

```bash
git switch feature/footer-2
git pull origin master       # Récupère master (avec le footer de collab-1) → conflit
```

- Ouvrez `index.html`, gardez **les deux footers** l'un sous l'autre, supprimez les marqueurs.
- Puis :
  ```bash
  git add index.html
  git commit -m "merge: combine les deux footers"
  git push
  ```

5. Retournez sur la PR : le conflit a disparu. Faites relire, puis fusionnez.

> Le commit de résolution doit avoir un message **explicite**, pas le message par défaut.
> GitHub propose aussi un bouton **Resolve conflicts** dans le navigateur ; ici on s'entraîne à le faire avec Git, car c'est ce qui marche dans tous les cas.

---

## Exercice 3.5 — `.gitignore` et `revert` (5 pts)

### Partie A — Ignorer des fichiers (2 pts) — collab-3

Certains fichiers ne doivent **jamais** être commités : logs, fichiers système, dépendances, secrets…

1. Branche `chore/gitignore`. Créez un fichier `.gitignore` :
   ```
   *.log
   .DS_Store
   node_modules/
   .env
   ```
2. Créez un fichier `debug.log` avec n'importe quel contenu.
3. `git status` : `debug.log` **n'apparaît pas**. Git l'ignore.
4. Commit du `.gitignore` uniquement, PR, review, fusion.

### Partie B — Annuler un commit sans réécrire l'historique (3 pts) — collab-2

On simule une erreur arrivée en production.

1. Branche `feature/titre-casse` : introduisez une faute dans le `h1` (ex. : `Le super nouveua site`). PR, review, **fusion** (oui, volontairement).
2. Le site est cassé ! Trouvez le commit fautif :
   ```bash
   git switch master && git pull
   git log --oneline
   ```
3. Annulez-le sur une nouvelle branche :
   ```bash
   git switch -c revert/titre-casse
   git revert <hash-du-commit-fautif>
   git push -u origin revert/titre-casse
   ```
4. PR, review, fusion.

> `git revert` crée un **nouveau commit** qui fait l'inverse du commit fautif. L'historique est conservé : personne n'est gêné.
> `git reset`, lui, **efface** des commits. Sur une branche partagée comme `master`, on utilise toujours `revert`.

---

## Ce qu'il faut retenir

```
 Issue  ──▶  branche + commits  ──▶  push  ──▶  Pull Request  ──▶  review  ──▶  merge  ──▶  pull
  🌐            💻 Git                💻→🌐        🌐                 🌐 + 💻       🌐          🌐→💻
```

- **Git** gère les versions, dans votre Codespace.
- **GitHub** organise le travail d'équipe : qui fait quoi, qui relit, quand on fusionne.
- **Codespaces** donne à chacun un environnement identique, pour coder **et** pour tester la branche des autres.

➡️ [Passer au niveau 4](niveau-4-avance.md)
