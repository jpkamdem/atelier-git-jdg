# Guillaume PAPALIA

- Pseudo GitHub : @Guillaume555
- Ce que je connais déjà de Git : 
git status
git push
git pull
git commit 
etc....


git commit -m "docs(equipe): ajoute la fiche d'Alice"git 

1. Juste après `git commit`, où se trouve mon commit ?
mon commit est sur ma machine en local 
2. Juste après `git push`, où se trouve-t-il ?
il se trouve en ligne sur le serveur github 
3. Que se passe-t-il si je supprime mon Codespace après un commit mais sans push ?
il est suprimé car il etait uniquements en local et une fois suprimer ça supprime les donné localg

Traitez l'urgence : créez une branche fix/urgence-<prenom>, ajoutez à votre fiche equipe/<prenom>.md une section ## Stash qui explique en 3 lignes à quoi sert git stash. Commit, push, PR :

`git stash` met de côté les modifications pas encore commitées comme une copie dans le press papier si on a une urgence, pour reprendre le travail d'une autre branche sans perdre notre travail. On récupère ensuite ses modifications avec `git stash pop`.