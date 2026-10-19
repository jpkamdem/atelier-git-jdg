# Guide enseignant

[⬅️ Retour au sommaire](../README.md)

## Préparer le dépôt

1. Ce dépôt doit être marqué comme **modèle** : **Settings → General → Template repository** ✔️.
   Les étudiants utilisent **Use this template** plutôt qu'un fork : leurs PR ciblent ainsi leur propre dépôt, et non celui de l'enseignant (erreur fréquente avec les forks).
2. Vérifiez que `index.html` est dans son état de départ (fautes présentes, `<ul>`, pas de `style.css`).
3. Ouvrez vous-même un Codespace une fois pour vérifier que le dev container démarre.

## Le site de départ contient

| Faute | Où | Corrigée au |
| --- | --- | --- |
| `l'éole` | `h2` | niveau 2 (collab-3) |
| `Feaubourg Saint Antoinette` | adresse | niveau 2 (collab-3) |
| `Hennnou` | directeur | niveau 2 (collab-3) |
| `Mon Sitte` | `<title>` | niveau 3 (`fix/titre`) |

## Conflits prévus

- **Niveau 2, étape 2** : `feature/contenu` contre `fix/fautes` (lignes de la liste).
- **Niveau 2, étape 3** : `feature/style` contre `master` (bloc `h2` + liste, à cause de `<ul>` → `<ol>`).
- **Niveau 3, exercice 3.4** : les deux footers.

## Ce que le dev container configure

- Extensions : Live Preview (aperçu du site), Git Graph, GitHub Pull Requests.
- Node.js (pour `npx htmlhint`, comme la CI).
- `GIT_EDITOR=code --wait` : les messages de merge et `rebase -i` s'ouvrent dans un onglet VS Code au lieu de vim.
- `pull.rebase false` : `git pull` fusionne par défaut, sans l'avertissement « divergent branches ».

## Points de vigilance

- **Quota Codespaces** : environ 60 h/mois sur une machine 2 cœurs en compte gratuit. Rappelez d'arrêter les Codespaces en fin de séance.
- **Protection de branche** : gratuite uniquement sur un dépôt **public** (sauf comptes Pro / Student Pack).
- **Groupe de 2** : collab-1 cumule les missions de collab-3.

## Grille de correction rapide

| Niveau | Où vérifier |
| --- | --- |
| 1 | `EQUIPE.md`, dossier `equipe/`, graphe des commits (`Insights → Network`) |
| 2 | Branches `feature/style`, `feature/contenu`, `fix/fautes` fusionnées ; commits de merge avec messages explicites |
| 3 | Onglet **Projects**, issues fermées par PR, reviews avec commentaires, `.gitignore`, commit `Revert "..."` |
| 4 | `devcontainer.json` modifié, section `## Stash` dans les fiches, PR `feature/meta`, onglet **Actions** (run rouge + vert), **Releases** v1.0.0 et v1.0.1 |
