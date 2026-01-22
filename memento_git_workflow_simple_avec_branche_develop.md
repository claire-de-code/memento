# Mémento Git — Commandes de base et workflow avec branche `develop`

Ce document est un aide-mémoire **sans icônes**, volontairement simple, pour travailler proprement avec Git, SSH et un workflow `develop → main`.

---

## Principes fondamentaux

- `main` : version stable, production
- `develop` : travail en cours
- On ne code jamais directement sur `main`
- La mise en ligne se fait uniquement via `main`

Schéma mental :

```
develop  --->  main  --->  production
   ↑
   travail quotidien
```

---

## Installer Git

### Linux (Debian / Ubuntu / Mint)

```bash
sudo apt update
sudo apt install git
```

### Linux (Arch / Manjaro / CachyOS)

```bash
sudo pacman -S git
```

### macOS (Homebrew)

```bash
brew install git
```

### Vérifier l’installation

```bash
git --version
```

---

## Configurer Git (une seule fois par machine)

### Identité utilisateur

```bash
git config --global user.name "Ton Nom"
git config --global user.email "ton@email.com"
git config --global push.autoSetupRemote true

```

Ces informations apparaissent dans l’historique des commits.

### Éditeur par défaut (optionnel)

Exemple avec `vim` :

```bash
git config --global core.editor vim
```

### Vérifier la configuration

```bash
git config --global --list
```

---

## Initialiser un projet Git (nouveau dossier)

### Créer un dossier et entrer dedans

```bash
mkdir mon-projet
cd mon-projet
```

### Initialiser Git

```bash
git init
```

### Créer un premier fichier

```bash
touch index.html
```

### Premier commit

```bash
git add .
git commit -m "chore: initialiser le projet"
```

---

## Créer un dépôt GitHub et le lier

### Via l’interface GitHub (classique)

Créer un dépôt vide sur GitHub, puis le lier :

```bash
git remote add origin git@github.com:USER/REPO.git
git branch -M main
git push -u origin main
```

###

#### Lier le dépôt créé

```bash
git remote add origin git@github.com:USERNAME/mon-projet.git
git branch -M main
git push -u origin main
```

---

## Configuration SSH (une seule fois par machine)

### Générer une clé SSH

```bash
ssh-keygen -t ed25519 -C "email@domaine.com"
```

Entrée pour tout accepter par défaut.

### Copier la clé publique

```bash
cat ~/.ssh/id_ed25519.pub
```

Ajouter cette clé dans GitHub : Settings → SSH and GPG keys → New SSH key

### Tester la connexion

```bash
ssh -T git@github.com
```

---

## Créer et utiliser la branche `develop`

### Création (une seule fois)

```bash
git checkout -b develop
git push -u origin develop
```

### Changer de branche

```bash
git checkout develop
git checkout main
```

---

## Cycle de travail quotidien

### Vérifier l’état

```bash
git status
```

### Ajouter les modifications

```bash
git add .
```

### Commit

```bash
git commit -m "feat: ajouter page en construction"
```

### Envoyer sur GitHub

```bash
git push
```

Tant que tu es sur `develop`, rien n’est déployé.

---

## Mettre en production (merge vers `main`)

```bash
git checkout main
git merge develop
git push
```

---

## Convention de messages de commit (recommandée)

Format :

```
type: description courte en français
```

Types utiles :

- feat : nouvelle fonctionnalité
- fix : correction de bug
- style : CSS / visuel uniquement
- docs : documentation
- chore : maintenance / configuration

Exemples :

```text
feat: ajouter page site en construction
style: améliorer lisibilité mobile
fix: corriger lien de contact
docs: ajouter instructions git
chore: nettoyer fichiers inutiles
```

---

## Modifier le message d’un commit

### Cas 1 — Modifier le **dernier commit** (le plus courant)

Si le commit n’est **pas encore poussé** ou même déjà poussé sur une branche de travail (`develop`) :

```bash
git commit --amend
```

- Git ouvre l’éditeur configuré (`vim`, `nano`, etc.)
- Modifie le texte du commit
- Enregistre et ferme l’éditeur

Pour changer **uniquement le message** sans toucher aux fichiers :

```bash
git commit --amend -m "feat: améliorer page en construction"
```

Si le commit était déjà poussé, il faudra ensuite :

```bash
git push --force-with-lease
```

---

### Cas 2 — Modifier un commit plus ancien

1. Afficher l’historique :

```bash
git log --oneline
```

2. Lancer un rebase interactif (exemple pour les 5 derniers commits) :

```bash
git rebase -i HEAD~5
```

3. Dans la liste, remplacer `pick` par `reword` (ou `r`) devant le commit à modifier
4. Enregistrer et fermer
5. Git ouvre l’éditeur pour modifier le message

Si la branche a déjà été poussée :

```bash
git push --force-with-lease
```

---

### Règles importantes

- Ne jamais réécrire l’historique partagé de `main`
- Autorisé sur `develop` ou branches personnelles
- Toujours utiliser `--force-with-lease` (jamais `--force`)

---

## Commandes utiles

### Voir l’historique

```bash
git log --oneline --graph
```

### Annuler un fichier ajouté

```bash
git reset fichier.html
```

### Supprimer un fichier suivi

```bash
git rm fichier.txt
```

---

## Erreurs à éviter

- Commiter sur `main`
- Messages vagues (update, test, fix)
- Gros commits non lisibles
- Travailler sans vérifier la branche active

---

## Règle d’or

`develop` est libre et évolutif.\
`main` est stable et propre.

Ce workflow est volontairement minimal. Il peut évoluer plus tard, mais il est suffisant pour 90 % des projets.

