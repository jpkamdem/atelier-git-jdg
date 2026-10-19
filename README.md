# Atelier Git, GitHub & Codespaces — travailler en équipe

Atelier pratique pour étudiants de **B3 Informatique**.
Vous allez construire à plusieurs un petit site web et, en chemin, apprendre à **versionner**, **partager** et **collaborer** comme dans une vraie équipe de développement.

---

## 1. Trois outils, trois rôles

Avant de commencer, retenez bien cette distinction : on la retrouvera à chaque étape.

| | **Git** 🔧 | **GitHub** 🌐 | **Codespaces** 💻 |
| --- | --- | --- | --- |
| **C'est quoi ?** | Un logiciel de gestion de versions | Un site web qui héberge des dépôts Git | Un ordinateur de développement dans le cloud |
| **Où ça tourne ?** | Sur la machine où vous tapez `git ...` | Sur les serveurs de GitHub (github.com) | Sur une machine virtuelle de GitHub, ouverte dans votre navigateur |
| **À quoi ça sert ?** | Enregistrer l'historique (commits), créer des branches, fusionner | Partager le dépôt, Issues, Pull Requests, reviews, CI, releases | Avoir VS Code + Git + les outils prêts à l'emploi, sans rien installer |
| **Exemple** | `git commit`, `git merge` | Ouvrir une Pull Request | Ouvrir un terminal et lancer `git status` |

Le point clé :

```
  Codespace d'Alice         Codespace de Bob          Codespace de Chloé
  (sa copie du dépôt)       (sa copie du dépôt)       (sa copie du dépôt)
        │  ▲                      │  ▲                       │  ▲
   push │  │ pull            push │  │ pull             push │  │ pull
        ▼  │                      ▼  │                       ▼  │
  ┌──────────────────────────────────────────────────────────────────┐
  │              Dépôt GitHub de l'équipe (la référence)             │
  └──────────────────────────────────────────────────────────────────┘
```

- **Chaque étudiant a son propre Codespace** = sa propre machine, avec **sa propre copie** du dépôt.
- Un `git commit` reste **dans votre Codespace**. Personne d'autre ne le voit.
- Un `git push` envoie vos commits **sur GitHub**. Un `git pull` récupère ceux des autres.
- Si vous supprimez votre Codespace sans avoir pushé, **votre travail est perdu**.

Dans les consignes, chaque action est marquée par l'endroit où elle se fait :

- 💻 **Codespace** : dans le terminal ou l'éditeur de votre Codespace
- 🌐 **GitHub** : sur le site github.com, dans votre navigateur

---

## 2. Organisation

- **Groupes de 3** (2 possible : voir les remarques dans chaque niveau).
- Chacun a un **compte GitHub**. Conseillé : activez le [GitHub Student Developer Pack](https://education.github.com/pack) (plus d'heures de Codespaces gratuites).
- Les niveaux se font **dans l'ordre** : chaque niveau utilise ce que vous avez appris au précédent.
- À la fin de chaque exercice, un **✅ Checkpoint** vous permet de vérifier que tout est bon avant de continuer.

> 💡 Un Codespace consomme votre quota gratuit tant qu'il est allumé. À la fin de la séance :
> 🌐 [github.com/codespaces](https://github.com/codespaces) → `...` → **Stop codespace**.

---

## 3. Le parcours

| Niveau | Thème | Ce que vous apprenez | Points |
| --- | --- | --- | --- |
| [**Niveau 0**](docs/niveau-0-demarrage.md) | Démarrer | Créer le dépôt de l'équipe, ouvrir son Codespace | — |
| [**Niveau 1**](docs/niveau-1-premiers-commits.md) | Premiers commits | `status`, `add`, `commit`, `log`, `diff`, `push`, `pull` | 20 |
| [**Niveau 2**](docs/niveau-2-branches.md) | Branches et fusions | `branch`, `switch`, `merge`, résoudre un conflit | 20 |
| [**Niveau 3**](docs/niveau-3-workflow-github.md) | Workflow GitHub | Issues, Project, Pull Requests, code review, `.gitignore`, `revert` | 30 |
| [**Niveau 4**](docs/niveau-4-avance.md) | Pratiques avancées | `stash`, `rebase -i`, `cherry-pick`, GitHub Actions, releases, config du Codespace | 20 |
| | Qualité (transversal) | Voir [barème qualité](#5-qualité-10-points) | 10 |
| | **Total** | | **100** |

📌 Gardez sous la main l'[**aide-mémoire Git**](docs/aide-memoire.md) : commandes, vocabulaire et solutions aux erreurs fréquentes.

👩‍🏫 Enseignants : voir le [guide enseignant](docs/guide-enseignant.md).

---

## 4. Le projet fil rouge

Le dépôt contient un mini-site (`index.html`) **volontairement imparfait** : des fautes, aucun style, peu de contenu.
Au fil des niveaux, votre équipe va le corriger, l'enrichir, ajouter des pages, une CI, et publier une version `v1.0.0`.

---

## 5. Qualité (10 points)

Notée sur l'ensemble de l'atelier :

- **Commits (4 pts)** — un commit = une idée ; messages clairs au format [Conventional Commits](https://www.conventionalcommits.org/fr/) :
  ```
  feat(contact): ajoute la page contact
  fix(index): corrige le nom du directeur
  chore(ci): ajoute un workflow de lint
  ```
- **Pull Requests (3 pts)** — titre clair, description avec le contexte, lien vers l'issue (`Closes #3`), capture d'écran si c'est visuel.
- **Reviews (3 pts)** — commentaires constructifs et concrets. Un simple « LGTM » ne compte pas.

---

## 6. Livraison finale

À la date limite, votre dépôt doit contenir :

- [ ] Le fichier `EQUIPE.md` et une fiche par membre dans `equipe/`
- [ ] Toutes les branches des niveaux 2 à 4 fusionnées dans `master`
- [ ] Au moins 4 issues fermées par des Pull Requests relues
- [ ] Une CI GitHub Actions **verte** sur `master`
- [ ] Deux releases publiées : `v1.0.0` et `v1.0.1`

Envoyez à votre enseignant :

- le **lien du dépôt** ;
- les **pseudos GitHub** des membres.

Bon atelier !
