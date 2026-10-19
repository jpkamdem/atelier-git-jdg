# Niveau 0 — Démarrer : le dépôt de l'équipe et vos Codespaces

⬅️ [Retour au sommaire](../README.md) · ➡️ [Niveau 1](niveau-1-premiers-commits.md)

**Durée indicative :** 20 min · **Non noté, mais obligatoire**

## Objectifs

- Créer **un** dépôt GitHub pour toute l'équipe.
- Donner accès à tous les membres.
- Que **chaque membre** ouvre **son propre** Codespace et découvre son environnement.

---

## Exercice 0.1 — Choisir les rôles

Mettez-vous d'accord sur l'ordre des membres. Il servira pour tout l'atelier :

| Rôle | Rôle en plus |
| --- | --- |
| **collab-1** | **Propriétaire** du dépôt (c'est lui qui le crée) |
| **collab-2** | |
| **collab-3** | |

> Groupe de 2 : collab-1 fera aussi les missions de collab-3.

---

## Exercice 0.2 — Créer le dépôt de l'équipe (collab-1 uniquement)

🌐 **GitHub**

1. Ouvrez le dépôt de l'enseignant.
2. Cliquez sur **Use this template** → **Create a new repository**.
3. Owner : **votre compte**. Nom : `atelier-git-<nom-equipe>`.
4. Visibilité : **Public** (nécessaire pour protéger la branche `master` au niveau 3 avec un compte gratuit).
5. **Create repository**.

> Vous avez maintenant une **copie indépendante** du projet sur votre compte.
> C'est ce dépôt qui sera la **référence commune** de l'équipe.

---

## Exercice 0.3 — Inviter les autres membres (collab-1 uniquement)

🌐 **GitHub**

1. Dans votre nouveau dépôt : **Settings** → **Collaborators** → **Add people**.
2. Ajoutez les pseudos GitHub de collab-2 et collab-3.
3. collab-2 et collab-3 **acceptent l'invitation** (reçue par email ou sur [github.com/notifications](https://github.com/notifications)).

✅ **Checkpoint** : collab-2 et collab-3 voient le dépôt et le bouton **Code** est vert pour eux.

---

## Exercice 0.4 — Ouvrir son Codespace (tout le monde)

🌐 **GitHub** — chacun **depuis son propre compte**, sur le dépôt de l'équipe :

1. Bouton vert **Code** → onglet **Codespaces** → **Create codespace on master**.
2. Patientez 1 à 2 minutes : un VS Code s'ouvre dans votre navigateur.

💻 **Codespace** — ouvrez le terminal (menu ☰ → **Terminal** → **New Terminal**) et tapez :

```bash
git --version        # Git est déjà installé dans le Codespace
git config user.name # Votre nom est déjà configuré (récupéré depuis GitHub)
git remote -v        # "origin" = l'adresse du dépôt de l'équipe sur GitHub
git log --oneline    # L'historique est déjà là : le Codespace contient un clone du dépôt
```

> 💡 Ce que vous venez de voir :
> - Le Codespace est une **machine Linux** qui vous est réservée.
> - GitHub y a fait automatiquement un `git clone` du dépôt de l'équipe.
> - `origin` est le **lien** entre votre copie (Codespace) et la référence (GitHub).

---

## Exercice 0.5 — Voir le site

💻 **Codespace**

1. Dans l'explorateur de fichiers à gauche, faites un clic droit sur `index.html` → **Show Preview**.
2. Le site s'affiche dans un onglet. Il contient des fautes : c'est normal, vous les corrigerez plus tard.

Repérez aussi l'icône **Source Control** (barre de gauche) et **Git Graph** (barre du bas) : on s'en servira pour visualiser l'historique.

---

## Exercice 0.6 — Mini-quiz (à l'oral, en groupe)

Répondez ensemble avant de passer au niveau suivant :

1. Combien de copies du dépôt existe-t-il maintenant dans votre équipe ? (indice : plus d'une !)
2. Si Alice modifie `index.html` dans son Codespace, Bob le voit-il ? Pourquoi ?
3. Lequel de ces trois outils pourrait être remplacé par votre propre ordinateur : Git, GitHub ou Codespaces ?

<details>
<summary>Réponses</summary>

1. **4 copies** (pour 3 membres) : une sur GitHub + une dans chaque Codespace.
2. **Non.** La modification est uniquement dans le Codespace d'Alice. Il faudra qu'elle fasse `commit` puis `push`, et que Bob fasse `pull`.
3. **Codespaces.** C'est juste un ordinateur dans le cloud. Avec Git et VS Code installés sur votre PC, vous feriez exactement la même chose.

</details>

---

✅ **Checkpoint final** : les 3 membres ont un Codespace ouvert sur le dépôt de l'équipe et voient le site.

➡️ [Passer au niveau 1](niveau-1-premiers-commits.md)
