# Niveau 1 — Premiers commits : ma copie, la copie des autres

⬅️ [Niveau 0](niveau-0-demarrage.md) · [Sommaire](../README.md) · ➡️ [Niveau 2](niveau-2-branches.md)

**Durée indicative :** 45 min · **20 points**

## Objectifs

- Maîtriser le cycle de base : **modifier → `add` → `commit`**.
- Comprendre qu'un commit est **local** (dans votre Codespace) tant qu'il n'est pas pushé.
- Synchroniser les Codespaces de l'équipe avec **`push`** et **`pull`**.

Dans ce niveau, tout le monde travaille directement sur `master`. C'est volontaire pour commencer simplement ; on verra au niveau 2 pourquoi on utilise des branches.

### Le cycle de base

```
  fichier modifié  ──git add──▶  zone de préparation  ──git commit──▶  historique local  ──git push──▶  GitHub
   (working tree)                    (staging)                          (votre Codespace)
```

---

## Exercice 1.1 — Présenter l'équipe (3 pts)

### collab-1 💻 Codespace

1. Créez le fichier `EQUIPE.md` à la racine :

   ```markdown
   # Notre équipe

   | Rôle | Nom Prénom | Pseudo GitHub |
   | --- | --- | --- |
   | collab-1 | ... | ... |
   | collab-2 | ... | ... |
   | collab-3 | ... | ... |

   Date de l'atelier : JJ/MM/AAAA
   ```

2. Enregistrez votre travail dans Git :

   ```bash
   git status                 # EQUIPE.md apparaît en rouge : Git le voit mais ne le suit pas encore
   git add EQUIPE.md
   git status                 # Il passe en vert : il est prêt à être commité
   git commit -m "docs: ajoute la présentation de l'équipe"
   git log --oneline          # Votre commit est en haut de l'historique
   ```

3. Allez voir le dépôt sur 🌐 **GitHub** : `EQUIPE.md` **n'y est pas**. Normal, le commit est seulement dans votre Codespace.
4. Envoyez-le :

   ```bash
   git push
   ```

5. Rafraîchissez la page GitHub : le fichier est là.

### collab-2 et collab-3 💻 Codespace

```bash
ls                 # EQUIPE.md n'existe pas chez vous
git pull           # Récupère les nouveaux commits depuis GitHub
ls                 # Il est là !
```

✅ **Checkpoint** : `EQUIPE.md` est visible sur GitHub et dans les 3 Codespaces.

---

## Exercice 1.2 — Ma fiche personnelle (8 pts)

Chacun, **dans son Codespace**, en même temps.

💻 **Codespace**

1. Créez le fichier `equipe/<votre-prenom>.md` (ex. : `equipe/alice.md`) :

   ```markdown
   # Alice Martin

   - Pseudo GitHub : @alice-m
   - Ce que je connais déjà de Git : ...
   ```

2. Commitez-le :

   ```bash
   git status
   git add equipe/alice.md
   git commit -m "docs(equipe): ajoute la fiche d'Alice"
   ```

3. Ajoutez une ligne à votre fiche :

   ```markdown
   - Ce que j'attends de cet atelier : ...
   ```

4. Avant de commiter, regardez **exactement** ce qui a changé :

   ```bash
   git diff            # Les lignes ajoutées sont précédées d'un +
   ```

5. Commitez cette modification :

   ```bash
   git add equipe/alice.md
   git commit -m "docs(equipe): ajoute les attentes d'Alice"
   git log --oneline   # Vous devez voir vos 2 commits
   ```

> ⚠️ **Ne pushez pas encore !** On va le faire tous ensemble à l'exercice suivant.

✅ **Checkpoint** : `git log --oneline` montre vos 2 commits, et `git status` affiche `Your branch is ahead of 'origin/master' by 2 commits`.
Traduction : « votre Codespace a 2 commits que GitHub ne connaît pas ».

---

## Exercice 1.3 — Push simultané : le premier gagne (6 pts)

1. **collab-1** fait `git push` → ✅ ça marche.
2. **collab-2** fait ensuite `git push` → ❌ refusé :

   ```
   ! [rejected]        master -> master (fetch first)
   error: failed to push some refs
   hint: Updates were rejected because the remote contains work that you do not have locally.
   ```

   **Pourquoi ?** GitHub contient maintenant les commits de collab-1, que collab-2 n'a pas. Git refuse d'écraser le travail de quelqu'un d'autre.

3. **collab-2** récupère d'abord le travail des autres, puis pushe :

   ```bash
   git pull     # Récupère les commits de collab-1 et les fusionne avec les vôtres
   git push     # Maintenant ça passe
   ```

   > Si un onglet s'ouvre avec un message `Merge branch 'master' of ...`, c'est Git qui vous demande de valider le message du commit de fusion. **Fermez simplement l'onglet** pour l'accepter.

4. **collab-3** fait la même chose : `git push` (refusé) → `git pull` → `git push`.
5. Tout le monde termine par un `git pull`.

Pas de conflit ici : chacun a modifié **un fichier différent**, Git sait fusionner tout seul.

Visualisez le résultat :

```bash
git log --oneline --graph --all
```

ou cliquez sur **Git Graph** dans la barre du bas. Vous voyez les historiques des 3 Codespaces qui se rejoignent.

✅ **Checkpoint** : dans chaque Codespace, le dossier `equipe/` contient les 3 fiches.

---

## Exercice 1.4 — Qui fait quoi ? (3 pts)

Chacun ajoute à la fin de **sa propre fiche** la réponse à ces 3 questions, puis commit + push (n'oubliez pas le `pull` si le push est refusé) :

```markdown
## Quiz

1. Juste après `git commit`, où se trouve mon commit ?
2. Juste après `git push`, où se trouve-t-il ?
3. Que se passe-t-il si je supprime mon Codespace après un commit mais sans push ?
```

---

## Ce qu'il faut retenir

| Commande | Où agit-elle ? | Effet |
| --- | --- | --- |
| `git add` | Codespace | Prépare un fichier pour le prochain commit |
| `git commit` | Codespace | Enregistre une version dans l'historique **local** |
| `git push` | Codespace → GitHub | Envoie vos commits sur GitHub |
| `git pull` | GitHub → Codespace | Récupère et fusionne les commits des autres |

**Règle d'or :** `git pull` avant de commencer à travailler, `git push` quand vous avez fini.

➡️ [Passer au niveau 2](niveau-2-branches.md)
