# Niveau 2 — Branches et fusions : travailler en parallèle

⬅️ [Niveau 1](niveau-1-premiers-commits.md) · [Sommaire](../README.md) · ➡️ [Niveau 3](niveau-3-workflow-github.md)

**Durée indicative :** 1 h · **20 points**

## Objectifs

- Créer une **branche** pour travailler sans gêner les autres.
- Publier sa branche sur GitHub.
- **Fusionner** (`merge`) les branches dans `master`.
- Résoudre un **conflit**.

### Pourquoi des branches ?

Au niveau 1, tout le monde poussait sur `master` : au moindre travail inachevé, tout le monde en hérite.
Une branche est une **ligne de travail parallèle**. On y travaille tranquillement, puis on la fusionne quand c'est prêt.

```
master          ●───●───────────────────●  (fusion)
                     \                 /
feature/style         ●───●───●───────
```

---

## Exercice 2.1 — Créer sa branche (2 pts)

💻 **Codespace** — chacun dans le sien :

```bash
git switch master
git pull                          # Toujours partir d'un master à jour
git switch -c <nom-de-branche>    # Crée la branche ET bascule dessus
git branch                        # La branche courante est marquée d'une *
```

| Membre | Branche |
| --- | --- |
| collab-1 | `feature/style` |
| collab-2 | `feature/contenu` |
| collab-3 | `fix/fautes` |

> Le nom de la branche courante est aussi affiché en bas à gauche de VS Code.

---

## Exercice 2.2 — Les missions en parallèle (10 pts)

Les 3 missions modifient **le même fichier** `index.html`. Faites **plusieurs petits commits** (un par modification), avec des messages clairs.

Pour voir le résultat : clic droit sur `index.html` → **Show Preview**.

### collab-1 — `feature/style` : donner du style

- Créer `style.css` et le lier dans le `<head>` de `index.html` :
  ```html
  <link rel="stylesheet" href="style.css">
  ```
- Titre `h1` en rouge.
- Titre `h2` en vert.
- Remplacer la liste à puces `<ul>` par une liste numérotée `<ol>`.

### collab-2 — `feature/contenu` : enrichir le contenu

- Ajouter un élément à la fin de la liste : `Prof de Git : Boris STOCKER`.
- Ajouter une courte description à **chaque** élément de la liste, sur ce modèle :
  ```html
  <li>Nom : ESGI<br><em>École Supérieure de Génie Informatique</em></li>
  ```

### collab-3 — `fix/fautes` : corriger les fautes

Corriger, avec **un commit par faute** :

- la faute dans le titre `h2` ;
- les fautes dans l'adresse (la vraie adresse est *242 Rue du Faubourg Saint-Antoine*) ;
- la faute dans le nom du directeur.

> Groupe de 2 : collab-1 fait aussi cette mission, sur une deuxième branche.

### Publier sa branche (tout le monde)

```bash
git push -u origin <nom-de-branche>
```

`-u` relie votre branche locale à celle de GitHub : les prochaines fois, un simple `git push` suffira.

✅ **Checkpoint** : 🌐 sur GitHub, le menu déroulant des branches (à gauche, au-dessus des fichiers) affiche 4 branches : `master`, `feature/style`, `feature/contenu`, `fix/fautes`.

---

## Exercice 2.3 — Fusionner, chacun son tour (8 pts)

On fusionne les 3 branches dans `master`, **dans cet ordre** et **chacun dans son Codespace**.
Attendez que le précédent ait pushé avant de commencer.

### Étape 1 — collab-3 fusionne `fix/fautes`

```bash
git switch master
git pull
git merge fix/fautes
git push
```

Git affiche `Fast-forward` : `master` n'avait pas bougé depuis la création de la branche, il suffit de « l'avancer ». Aucun conflit possible.

### Étape 2 — collab-2 fusionne `feature/contenu`

```bash
git switch master
git pull                  # Récupère la fusion de collab-3
git merge feature/contenu
```

💥 **Conflit !**

```
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

collab-3 a corrigé l'adresse et le directeur, et vous avez ajouté des descriptions **sur les mêmes lignes**. Git ne sait pas quelle version garder : c'est à vous de décider.

Ouvrez `index.html`. Git a inséré des marqueurs (votre contenu peut varier un peu) :

```html
<<<<<<< HEAD
      <li>Nom : ESGI</li>
      <li>Adresse : 242 Rue du Faubourg Saint-Antoine, 75011 Paris</li>
      <li>Directeur : Kamal Hennou</li>
=======
      <li>Nom : ESGI<br><em>École Supérieure de Génie Informatique</em></li>
      <li>Adresse : 242 Rue du Feaubourg Saint Antoinette, 75011 Paris<br><em>Un super emplacement !</em></li>
      <li>Directeur : Kamal Hennnou<br><em>Un super directeur</em></li>
      <li>Prof de Git : Boris STOCKER<br><em>Un super prof !</em></li>
>>>>>>> feature/contenu
```

- Entre `<<<<<<< HEAD` et `=======` : la version de `master` (avec les corrections de collab-3).
- Entre `=======` et `>>>>>>>` : votre version (avec les descriptions, mais encore les fautes).

**Résolvez** en écrivant les bonnes lignes (corrections **et** descriptions), puis **supprimez les 3 marqueurs** :

```html
      <li>Nom : ESGI<br><em>École Supérieure de Génie Informatique</em></li>
      <li>Adresse : 242 Rue du Faubourg Saint-Antoine, 75011 Paris<br><em>Un super emplacement !</em></li>
      <li>Directeur : Kamal Hennou<br><em>Un super directeur</em></li>
      <li>Prof de Git : Boris STOCKER<br><em>Un super prof !</em></li>
```

> 💡 VS Code propose des boutons au-dessus du conflit (*Accept Current Change*, *Accept Incoming Change*, *Accept Both Changes*). Ici, aucun ne suffit seul : il faut éditer à la main.

Vérifiez qu'il ne reste aucun marqueur dans le fichier, puis :

```bash
git add index.html
git commit -m "merge: intègre feature/contenu en gardant les corrections"
git push
```

### Étape 3 — collab-1 fusionne `feature/style`

Même procédure (`switch`, `pull`, `merge`, résoudre si besoin, `add`, `commit`, `push`).
Le résultat doit garder **toutes** les modifications : corrections, descriptions **et** style.

> 💡 Ici, le conflit porte sur toute la liste. Le plus simple : gardez la version `HEAD` (déjà corrigée et enrichie), puis remplacez juste `<ul>`/`</ul>` par `<ol>`/`</ol>`.
> Le `<link>` vers `style.css` dans le `<head>` est fusionné automatiquement : Git ne signale un conflit que si les mêmes lignes ont été modifiées des deux côtés.

<details>
<summary>Résultat attendu (à ouvrir uniquement pour vérifier)</summary>

```html
<!doctype html>
<html lang="fr">
<head>
  <meta charset="utf-8">
  <title>Mon Sitte</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Le super nouveau site de l'école</h1>
  <section>
    <h2>Informations de l'école :</h2>
    <ol>
      <li>Nom : ESGI<br><em>École Supérieure de Génie Informatique</em></li>
      <li>Adresse : 242 Rue du Faubourg Saint-Antoine, 75011 Paris<br><em>Un super emplacement !</em></li>
      <li>Directeur : Kamal Hennou<br><em>Un super directeur</em></li>
      <li>Prof de Git : Boris STOCKER<br><em>Un super prof !</em></li>
    </ol>
  </section>
</body>
</html>
```

(Le titre de l'onglet contient encore une faute : elle sera corrigée au niveau 3.)

</details>

✅ **Checkpoint** :

- Tout le monde fait `git switch master && git pull` : les 3 Codespaces ont le même `index.html`.
- `git log --oneline --graph` (ou **Git Graph**) montre les 3 branches qui rejoignent `master`.
- Plus aucun marqueur `<<<<<<<`, `=======` ou `>>>>>>>` dans le fichier.

---

## Ce qu'il faut retenir

| Commande | Effet |
| --- | --- |
| `git switch -c ma-branche` | Crée une branche et bascule dessus |
| `git switch master` | Revient sur `master` |
| `git push -u origin ma-branche` | Publie la branche sur GitHub |
| `git merge ma-branche` | Fusionne `ma-branche` **dans la branche courante** |

Un **conflit** n'est pas une erreur : c'est Git qui vous demande de choisir quand deux personnes ont modifié les mêmes lignes.

> Jusqu'ici, n'importe qui pouvait fusionner n'importe quoi dans `master`, sans que personne relise. En entreprise, c'est risqué. Au niveau 3, on passe par **GitHub** pour relire avant de fusionner.

➡️ [Passer au niveau 3](niveau-3-workflow-github.md)
