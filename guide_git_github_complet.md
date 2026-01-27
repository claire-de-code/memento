# 📚 Guide Git & GitHub Complet pour Développeur Solo

**Pour qui ?** Développeur solo, junior ou amateur  
**Objectif :** Maîtriser Git de A à Z avec des explications simples et des exemples concrets

---

## 📋 Table des matières

1. [Comprendre Git et GitHub](#comprendre-git-et-github)
2. [Installation et configuration](#installation-et-configuration)
3. [Les concepts fondamentaux](#les-concepts-fondamentaux)
4. [Démarrer un projet](#démarrer-un-projet)
5. [Workflow quotidien](#workflow-quotidien)
6. [Gestion des branches](#gestion-des-branches)
7. [Workflow develop → main](#workflow-develop--main)
8. [SSH et sécurité](#ssh-et-sécurité)
9. [Commandes essentielles](#commandes-essentielles)
10. [Résoudre les problèmes courants](#résoudre-les-problèmes-courants)
11. [Bonnes pratiques](#bonnes-pratiques)
12. [Aller plus loin](#aller-plus-loin)

---

## Comprendre Git et GitHub

### Qu'est-ce que Git ?

**Git** est un système de **contrôle de version**. En termes simples :
- Il sauvegarde l'historique complet de ton projet
- Tu peux revenir en arrière à n'importe quel moment
- Tu peux expérimenter sans risque de tout casser
- C'est comme un "Ctrl+Z" super-puissant pour tout ton projet

**Analogie :** Imagine un jeu vidéo avec des points de sauvegarde. Git crée ces points de sauvegarde (appelés "commits"), et tu peux charger n'importe quelle sauvegarde quand tu veux.

### Qu'est-ce que GitHub ?

**GitHub** est un **hébergeur** de projets Git sur Internet :
- C'est le "cloud" pour ton code
- Tes projets sont sauvegardés en ligne
- Tu peux y accéder de n'importe où
- C'est gratuit pour les projets publics et privés

**Analogie :** Si Git est Word (sur ton ordinateur), GitHub est Google Drive (en ligne).

### Git vs GitHub

| Git | GitHub |
|-----|--------|
| Programme sur ton ordinateur | Site web en ligne |
| Fonctionne hors ligne | Nécessite Internet |
| Gratuit et open-source | Service gratuit (avec options payantes) |
| Enregistre l'historique local | Stocke ton code en ligne |

**En résumé :** Git = outil, GitHub = plateforme d'hébergement.

---

## Installation et configuration

### Installer Git

#### Linux (Debian/Ubuntu/Mint)
```bash
sudo apt update
sudo apt install git
```

#### Linux (Arch/Manjaro/CachyOS)
```bash
sudo pacman -S git
```

#### macOS
```bash
# Via Homebrew (recommandé)
brew install git

# Ou via Xcode Command Line Tools
xcode-select --install
```

#### Windows
1. Télécharge depuis [git-scm.com](https://git-scm.com/download/win)
2. Lance l'installateur
3. Accepte les options par défaut
4. Utilise **Git Bash** (terminal inclus)

### Vérifier l'installation

```bash
git --version
```

**Sortie attendue :** `git version 2.x.x`

### Configuration initiale (obligatoire)

**Pourquoi ?** Git a besoin de savoir qui tu es pour signer tes commits.

```bash
# Ton nom (apparaîtra dans l'historique)
git config --global user.name "Ton Nom"

# Ton email (celui de ton compte GitHub)
git config --global user.email "ton@email.com"

# Branche par défaut = main (standard moderne)
git config --global init.defaultBranch main

# Push automatique sans spécifier la branche
git config --global push.autoSetupRemote true

# Améliorer l'affichage des couleurs
git config --global color.ui auto
```

### Vérifier la configuration

```bash
git config --global --list
```

**Sortie :**
```
user.name=Ton Nom
user.email=ton@email.com
init.defaultbranch=main
push.autosetupremote=true
```

### Configurer l'éditeur de texte (optionnel mais recommandé)

Git utilise un éditeur pour écrire les messages de commit.

```bash
# Vim (si tu es à l'aise)
git config --global core.editor vim

# Nano (plus simple pour débuter)
git config --global core.editor nano

# VS Code (si installé)
git config --global core.editor "code --wait"
```

---

## Les concepts fondamentaux

### 1. Le dépôt (repository)

**Définition :** Un dossier suivi par Git.

```
mon-projet/
├── .git/           ← Dossier caché de Git (ne jamais toucher)
├── index.html
├── style.css
└── script.js
```

Le dossier `.git` contient tout l'historique. Si tu le supprimes, tu perds tout.

### 2. Les trois zones de Git

Git organise les fichiers en 3 zones :

```
┌─────────────────┐
│  Working Dir    │  ← Ton dossier de travail (fichiers visibles)
│  (modifié)      │
└────────┬────────┘
         │ git add
         ▼
┌─────────────────┐
│  Staging Area   │  ← Zone de préparation (index)
│  (prêt à commit)│
└────────┬────────┘
         │ git commit
         ▼
┌─────────────────┐
│  Repository     │  ← Historique permanent (commits)
│  (.git)         │
└─────────────────┘
```

**Workflow :**
1. Tu modifies des fichiers (working directory)
2. Tu les ajoutes au staging avec `git add`
3. Tu crées un commit avec `git commit`

**Analogie :** 
- Working dir = ton bureau
- Staging = une boîte où tu prépares ton colis
- Repository = l'entrepôt où tu envoies le colis

### 3. Le commit

**Définition :** Un point de sauvegarde avec un message descriptif.

Chaque commit contient :
- L'état exact de tous tes fichiers à ce moment
- Un message décrivant ce qui a changé
- L'auteur et la date
- Un identifiant unique (hash SHA)

```bash
# Exemple de commit
commit a3f5b2c9d8e7f1a2b3c4d5e6f7a8b9c0d1e2f3a4
Author: Ton Nom <ton@email.com>
Date:   Mon Jan 27 10:30:00 2025 +0100

    feat: ajouter page d'accueil
```

### 4. Les branches

**Définition :** Une ligne de développement parallèle.

```
main      : A --- B --- C --- F         (stable)
                   \           /
develop   :         D --- E ---         (travail)
```

**Analogie :** Imagine écrire un livre. La branche `main` est ta version publiée, `develop` est ton brouillon où tu expérimentes.

### 5. Local vs Remote

```
┌───────────────────┐         ┌───────────────────┐
│  Local (ton PC)   │         │  Remote (GitHub)  │
│                   │         │                   │
│  .git/            │ ◄──┬──► │  origin/main      │
│  main             │    │    │  origin/develop   │
│  develop          │    │    │                   │
└───────────────────┘    │    └───────────────────┘
                         │
                    git push / pull
```

- **Local :** Sur ton ordinateur
- **Remote :** Sur GitHub (appelé "origin" par convention)

---

## Démarrer un projet

### Option 1 : Nouveau projet local → GitHub

#### Étape 1 : Créer le projet localement

```bash
# Créer le dossier
mkdir mon-projet
cd mon-projet

# Initialiser Git
git init

# Créer un fichier
echo "# Mon Projet" > README.md

# Premier commit
git add .
git commit -m "chore: initialiser le projet"
```

**Explication :**
- `git init` crée le dossier `.git`
- `git add .` ajoute tous les fichiers au staging
- `git commit -m "..."` crée le premier commit

#### Étape 2 : Créer le dépôt sur GitHub

1. Va sur [github.com](https://github.com)
2. Clique sur **New repository**
3. Nom : `mon-projet`
4. **Ne coche RIEN** (pas de README, .gitignore, ou license)
5. Clique sur **Create repository**

#### Étape 3 : Lier local et GitHub

GitHub t'affiche les commandes. Copie-les :

```bash
git remote add origin git@github.com:USERNAME/mon-projet.git
git branch -M main
git push -u origin main
```

**Explication :**
- `git remote add origin ...` : définit l'URL du dépôt distant
- `git branch -M main` : renomme la branche en "main" (si besoin)
- `git push -u origin main` : envoie le code sur GitHub

**Vérification :**
```bash
git remote -v
```

**Sortie :**
```
origin  git@github.com:USERNAME/mon-projet.git (fetch)
origin  git@github.com:USERNAME/mon-projet.git (push)
```

### Option 2 : Cloner un projet existant

```bash
# Clone le dépôt
git clone git@github.com:USERNAME/mon-projet.git

# Entre dans le dossier
cd mon-projet

# Vérifier l'état
git status
```

**Explication :** `git clone` télécharge le projet complet avec tout son historique.

---

## Workflow quotidien

### Vue d'ensemble

```
1. Modifier des fichiers
   ↓
2. git status (vérifier)
   ↓
3. git add . (ajouter au staging)
   ↓
4. git commit -m "..." (créer un commit)
   ↓
5. git push (envoyer sur GitHub)
```

### Étape par étape

#### 1. Vérifier sur quelle branche tu es

```bash
git branch
```

**Sortie :**
```
  main
* develop    ← L'étoile indique la branche active
```

Si tu es sur `main` par erreur :
```bash
git checkout develop
```

#### 2. Vérifier l'état du projet

```bash
git status
```

**Sortie possible :**
```
On branch develop
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  
	modified:   index.html
	modified:   style.css

Untracked files:
  (use "git add <file>..." to include in what will be committed)
  
	script.js
```

**Interprétation :**
- `modified` : fichiers modifiés (déjà suivis par Git)
- `Untracked` : nouveaux fichiers (jamais ajoutés à Git)

#### 3. Ajouter les fichiers au staging

```bash
# Ajouter TOUS les fichiers modifiés
git add .

# OU ajouter des fichiers spécifiques
git add index.html style.css
```

**Vérifier à nouveau :**
```bash
git status
```

**Sortie :**
```
On branch develop
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
  
	modified:   index.html
	modified:   style.css
	new file:   script.js
```

Les fichiers sont maintenant "staged" (prêts à être commités).

#### 4. Créer un commit

```bash
git commit -m "feat: ajouter formulaire de contact"
```

**Convention des messages :** (voir section "Bonnes pratiques")
- `feat:` nouvelle fonctionnalité
- `fix:` correction de bug
- `style:` changements CSS/visuels
- `docs:` documentation
- `chore:` maintenance

**Exemples de bons messages :**
```
feat: ajouter page d'accueil
fix: corriger lien cassé dans le menu
style: améliorer responsive mobile
docs: ajouter README
chore: nettoyer fichiers de test
```

**Exemples de mauvais messages :**
```
update          ← Trop vague
test            ← Pas descriptif
fix             ← Quelle correction ?
modif page      ← Manque de contexte
```

#### 5. Envoyer sur GitHub

```bash
git push
```

**Si c'est ton premier push sur cette branche :**
```bash
git push -u origin develop
```

**Explication :**
- `-u` (ou `--set-upstream`) lie la branche locale à la branche distante
- Après ça, un simple `git push` suffira

### Workflow complet en une fois

```bash
git status                              # Vérifier
git add .                               # Ajouter
git commit -m "feat: ajouter footer"   # Commiter
git push                                # Pousser
```

---

## Gestion des branches

### Pourquoi les branches ?

Les branches permettent de :
- Travailler sur plusieurs fonctionnalités en parallèle
- Isoler les expérimentations
- Garder `main` stable

### Lister les branches

```bash
# Branches locales
git branch

# Branches locales ET distantes
git branch -a
```

### Créer une branche

```bash
# Créer et basculer en une commande
git checkout -b ma-branche

# OU en deux commandes
git branch ma-branche     # Créer
git checkout ma-branche   # Basculer
```

**Nouvelle syntaxe (Git 2.23+) :**
```bash
git switch -c ma-branche
```

### Basculer entre branches

```bash
git checkout main
git checkout develop

# Nouvelle syntaxe
git switch main
```

### Voir la branche active

```bash
git branch
```

**Sortie :**
```
  main
* develop    ← Tu es ici
  feature-login
```

### Renommer une branche

```bash
# Renommer la branche courante
git branch -m nouveau-nom

# Renommer une autre branche
git branch -m ancien-nom nouveau-nom
```

### Supprimer une branche

```bash
# Supprimer localement (branche mergée)
git branch -d ma-branche

# Forcer la suppression (même si non mergée)
git branch -D ma-branche

# Supprimer sur GitHub
git push origin --delete ma-branche
```

---

## Workflow develop → main

### Principe

```
develop  ──┬──► main  ──► Production/Déploiement
           │
    Travail quotidien
```

**Règles :**
1. **Jamais** coder directement sur `main`
2. Tout le développement se fait sur `develop`
3. `main` ne reçoit que du code testé et fonctionnel
4. Le déploiement se fait toujours depuis `main`

### Setup initial (une seule fois)

```bash
# Vérifier que tu es sur main
git checkout main

# Créer develop à partir de main
git checkout -b develop

# Envoyer develop sur GitHub
git push -u origin develop
```

### Workflow quotidien

#### 1. Travailler sur develop

```bash
# Basculer sur develop
git checkout develop

# Vérifier que c'est bien à jour
git pull

# Travailler normalement
# ... modifier des fichiers ...

# Commit et push
git add .
git commit -m "feat: ajouter système de login"
git push
```

#### 2. Mettre en production (merge vers main)

Quand `develop` est stable et prêt :

```bash
# Basculer sur main
git checkout main

# Mettre à jour main (au cas où)
git pull

# Fusionner develop dans main
git merge develop

# Pousser sur GitHub
git push
```

**Explication :**
- `git merge develop` : fusionne les commits de `develop` dans `main`
- Après le push, ton site/app peut être déployé depuis `main`

#### 3. Retourner sur develop

```bash
git checkout develop
```

### Visualiser l'historique

```bash
git log --oneline --graph --all
```

**Sortie :**
```
* a3f5b2c (HEAD -> develop) feat: ajouter formulaire
* d7e8f9a fix: corriger bug menu
| * b2c3d4e (main) chore: mise en prod v1.0
|/
* e1f2a3b docs: ajouter README
```

### Workflow complet exemple

```bash
# Jour 1 : développement
git checkout develop
git pull
# ... coder ...
git add .
git commit -m "feat: ajouter page contact"
git push

# Jour 2 : développement
# ... coder ...
git add .
git commit -m "fix: corriger responsive"
git push

# Jour 3 : mise en production
git checkout main
git pull
git merge develop
git push
# → Déploiement automatique ou manuel

# Retour au développement
git checkout develop
```

---

## SSH et sécurité

### Pourquoi SSH ?

SSH (Secure Shell) permet de :
- Se connecter à GitHub sans taper ton mot de passe
- Sécuriser les communications (chiffrement)
- Automatiser les push/pull

**Alternative :** HTTPS (nécessite un token à chaque fois, moins pratique)

### Vérifier si tu as déjà une clé SSH

```bash
ls -la ~/.ssh
```

**Si tu vois `id_ed25519` et `id_ed25519.pub` :** tu as déjà une clé, passe à "Ajouter à GitHub"

### Générer une clé SSH

```bash
ssh-keygen -t ed25519 -C "ton@email.com"
```

**Dialogue :**
```
Enter file in which to save the key (/home/user/.ssh/id_ed25519):
→ Appuie sur Entrée (accepte le chemin par défaut)

Enter passphrase (empty for no passphrase):
→ Appuie sur Entrée (pas de phrase de passe)

Enter same passphrase again:
→ Appuie sur Entrée
```

**Note :** Tu peux ajouter une phrase de passe pour plus de sécurité, mais ce n'est pas obligatoire.

### Démarrer l'agent SSH

```bash
# Démarrer l'agent
eval "$(ssh-agent -s)"

# Ajouter la clé
ssh-add ~/.ssh/id_ed25519
```

### Copier la clé publique

```bash
cat ~/.ssh/id_ed25519.pub
```

**Sortie :**
```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJl3d... ton@email.com
```

**Copie tout le texte** (depuis `ssh-ed25519` jusqu'à ton email).

### Ajouter la clé à GitHub

1. Va sur [github.com](https://github.com) et connecte-toi
2. Clique sur ton **avatar** (en haut à droite) → **Settings**
3. Dans le menu de gauche : **SSH and GPG keys**
4. Clique sur **New SSH key**
5. Titre : `Mon PC` (ou le nom de ta machine)
6. Key : colle la clé publique copiée
7. Clique sur **Add SSH key**

### Tester la connexion

```bash
ssh -T git@github.com
```

**Première fois :**
```
The authenticity of host 'github.com' can't be established.
Are you sure you want to continue connecting (yes/no)?
→ Tape "yes" et Entrée
```

**Sortie attendue :**
```
Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```

✅ Si tu vois ça, SSH fonctionne !

### Convertir un dépôt HTTPS vers SSH

Si tu as cloné avec HTTPS :
```bash
git remote set-url origin git@github.com:USERNAME/REPO.git
```

Vérifier :
```bash
git remote -v
```

**Sortie :**
```
origin  git@github.com:USERNAME/REPO.git (fetch)
origin  git@github.com:USERNAME/REPO.git (push)
```

---

## Commandes essentielles

### Statut et historique

```bash
# État actuel
git status

# Historique simplifié
git log --oneline

# Historique avec graphe
git log --oneline --graph --all

# Derniers 5 commits
git log --oneline -5

# Voir les modifications d'un commit
git show a3f5b2c
```

### Voir les différences

```bash
# Différences non stagées (working dir vs staging)
git diff

# Différences stagées (staging vs dernier commit)
git diff --staged

# Différences d'un fichier spécifique
git diff index.html

# Différences entre deux commits
git diff a3f5b2c d7e8f9a
```

### Annuler des modifications

#### Fichier modifié (non ajouté au staging)

```bash
# Annuler les modifications d'un fichier
git restore index.html

# Annuler TOUS les fichiers modifiés
git restore .
```

**Ancienne syntaxe :**
```bash
git checkout -- index.html
```

#### Fichier ajouté au staging (mais pas commité)

```bash
# Retirer du staging (garde les modifications)
git restore --staged index.html

# Retirer TOUS les fichiers du staging
git restore --staged .
```

**Ancienne syntaxe :**
```bash
git reset index.html
```

#### Annuler le dernier commit (mais garder les modifications)

```bash
git reset --soft HEAD~1
```

**Explication :**
- `--soft` : annule le commit mais garde les fichiers dans le staging
- `HEAD~1` : le commit précédent (1 commit en arrière)

#### Annuler le dernier commit (et perdre les modifications)

```bash
git reset --hard HEAD~1
```

⚠️ **ATTENTION :** `--hard` supprime définitivement les modifications !

### Modifier le dernier commit

#### Modifier le message

```bash
git commit --amend
```

Vim s'ouvre, modifie le message, enregistre et ferme.

**Version rapide :**
```bash
git commit --amend -m "feat: nouveau message corrigé"
```

#### Ajouter des fichiers oubliés

```bash
# Oubli : tu as commité sans un fichier
git add fichier-oublie.js
git commit --amend --no-edit
```

`--no-edit` garde le même message.

### Récupérer un fichier d'un ancien commit

```bash
# Voir l'historique
git log --oneline

# Récupérer le fichier d'un commit spécifique
git checkout a3f5b2c -- index.html
```

### Ignorer des fichiers (.gitignore)

Créer un fichier `.gitignore` à la racine :

```bash
# Ignorer node_modules
node_modules/

# Ignorer les fichiers de config
.env
config.local.js

# Ignorer les logs
*.log

# Ignorer les fichiers OS
.DS_Store
Thumbs.db

# Ignorer le dossier de build
dist/
build/
```

**Appliquer immédiatement :**
```bash
git add .gitignore
git commit -m "chore: ajouter .gitignore"
```

---

## Résoudre les problèmes courants

### Problème 1 : "fatal: not a git repository"

**Cause :** Tu n'es pas dans un dépôt Git.

**Solution :**
```bash
# Vérifier le dossier actuel
pwd

# Soit initialiser Git
git init

# Soit aller dans le bon dossier
cd /chemin/vers/mon-projet
```

### Problème 2 : "Updates were rejected"

**Message complet :**
```
! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'github.com:...'
```

**Cause :** Quelqu'un (ou toi depuis un autre PC) a poussé sur GitHub pendant que tu travaillais.

**Solution :**
```bash
# Récupérer les changements
git pull

# Puis pousser à nouveau
git push
```

**Si conflit :** voir "Problème 4".

### Problème 3 : J'ai commité sur main au lieu de develop

**Solution :**
```bash
# Noter le hash du commit (par exemple a3f5b2c)
git log --oneline

# Annuler le commit sur main (garde les fichiers)
git reset --soft HEAD~1

# Basculer sur develop
git checkout develop

# Re-commiter
git add .
git commit -m "feat: mon commit"
git push
```

### Problème 4 : Conflit de fusion (merge conflict)

**Situation :**
```bash
git pull
# ou
git merge develop
```

**Message :**
```
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

**Solution étape par étape :**

1. **Ouvrir le fichier en conflit**

Le fichier contient des marqueurs :
```html
<!DOCTYPE html>
<html>
<<<<<<< HEAD
<head><title>Mon Site v1</title></head>
=======
<head><title>Mon Super Site</title></head>
>>>>>>> develop
<body>
```

**Explication :**
- `<<<<<<< HEAD` : version actuelle (branche où tu es)
- `=======` : séparateur
- `>>>>>>> develop` : version de l'autre branche

2. **Choisir la bonne version**

Supprime les marqueurs et garde ce que tu veux :
```html
<!DOCTYPE html>
<html>
<head><title>Mon Super Site</title></head>
<body>
```

3. **Marquer comme résolu**
```bash
git add index.html
git commit -m "fix: résoudre conflit de fusion"
git push
```

### Problème 5 : J'ai fait un commit avec le mauvais message

**Si non poussé :**
```bash
git commit --amend -m "feat: nouveau message correct"
```

**Si déjà poussé sur develop (pas sur main) :**
```bash
git commit --amend -m "feat: nouveau message correct"
git push --force-with-lease
```

⚠️ **JAMAIS sur main** ! Uniquement sur tes branches de travail.

### Problème 6 : "Permission denied (publickey)"

**Cause :** SSH mal configuré.

**Solution :**
```bash
# Vérifier les clés
ls ~/.ssh

# Si pas de clé, en générer une
ssh-keygen -t ed25519 -C "ton@email.com"

# Ajouter à l'agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Copier et ajouter à GitHub
cat ~/.ssh/id_ed25519.pub

# Tester
ssh -T git@github.com
```

### Problème 7 : J'ai supprimé un fichier par erreur

**Si pas encore commité :**
```bash
git restore fichier.js
```

**Si déjà commité :**
```bash
# Trouver le commit où le fichier existait
git log --oneline -- fichier.js

# Récupérer depuis ce commit
git checkout a3f5b2c -- fichier.js

# Commiter la récupération
git add fichier.js
git commit -m "fix: récupérer fichier supprimé"
```

### Problème 8 : J'ai tout cassé, je veux recommencer

**Solution ultime (annule TOUT) :**
```bash
# Annuler toutes les modifications non commitées
git reset --hard HEAD

# Revenir au dernier commit
git clean -fd
```

⚠️ **ATTENTION :** Perte définitive de toutes les modifications non commitées !

---

## Bonnes pratiques

### 1. Messages de commit

#### Convention Conventional Commits

Format :
```
<type>: <description>

[optionnel] <corps>
[optionnel] <footer>
```

**Types courants :**

| Type | Usage | Exemple |
|------|-------|---------|
| `feat` | Nouvelle fonctionnalité | `feat: ajouter page contact` |
| `fix` | Correction de bug | `fix: corriger lien cassé` |
| `style` | CSS/visuel uniquement | `style: améliorer responsive` |
| `refactor` | Refactorisation code | `refactor: simplifier fonction login` |
| `docs` | Documentation | `docs: ajouter README` |
| `test` | Tests | `test: ajouter tests unitaires` |
| `chore` | Maintenance | `chore: mettre à jour dépendances` |
| `perf` | Performance | `perf: optimiser chargement images` |

**Exemples concrets :**
```
feat: ajouter système de login utilisateur
fix: corriger affichage menu mobile
style: améliorer contraste des boutons
docs: ajouter instructions d'installation
chore: configurer ESLint
refactor: restructurer composant Header
perf: lazy loading des images
test: ajouter tests pour API
```

**Mauvais exemples :**
```
update           ← Trop vague
fix              ← Quelle correction ?
test commit      ← Pas informatif
modif            ← Incompréhensible
```

### 2. Fréquence des commits

**Règle :** Commit souvent, petits commits.

**Bon rythme :**
- ✅ 1 commit = 1 fonctionnalité logique
- ✅ Plusieurs commits par jour
- ✅ Commit avant de tester une idée risquée

**Mauvais rythme :**
- ❌ 1 énorme commit par semaine
- ❌ "update" avec 50 fichiers modifiés
- ❌ Jamais de commit pendant 3 jours

**Exemple de bonne journée :**
```
10h00: feat: créer structure HTML page contact
11h30: feat: ajouter formulaire avec validation
14h00: style: styler formulaire responsive
15h30: fix: corriger validation email
16h00: docs: documenter champs formulaire
```

### 3. Organisation des branches

**Workflow minimal (solo) :**
```
main     ← Version stable/production
develop  ← Développement quotidien
```

**Workflow avec fonctionnalités :**
```
main
 └─ develop
     ├─ feature/login
     ├─ feature/contact-form
     └─ bugfix/menu-mobile
```

**Nommage des branches :**
```
feature/nom-fonctionnalite   ← Nouvelles fonctionnalités
bugfix/nom-bug               ← Corrections
hotfix/nom-urgence           ← Corrections urgentes en prod
experiment/nom-test          ← Expérimentations
```

**Exemples :**
```
feature/user-authentication
feature/dark-mode
bugfix/broken-navbar
hotfix/critical-security-issue
experiment/new-design
```

### 4. Que mettre dans .gitignore

```gitignore
# Dépendances
node_modules/
vendor/
venv/

# Fichiers de build
dist/
build/
*.min.js
*.min.css

# Configuration locale
.env
.env.local
config.local.js

# Logs
*.log
logs/

# Fichiers OS
.DS_Store
Thumbs.db
desktop.ini

# IDE
.vscode/
.idea/
*.swp
*.swo

# Cache
.cache/
*.tmp

# Fichiers sensibles
*.key
*.pem
secrets.json
```

### 5. Avant de pousser sur main

**Checklist :**
- [ ] Le code fonctionne
- [ ] Pas d'erreurs dans la console
- [ ] Testé sur différents navigateurs (si web)
- [ ] Messages de commit clairs
- [ ] `.gitignore` à jour
- [ ] Pas de fichiers sensibles (.env, mots de passe)

### 6. Workflow équipe (bonus pour plus tard)

**Pull Request (PR) :**
1. Travaille sur une branche feature
2. Pousse sur GitHub
3. Crée une Pull Request vers develop
4. Demande une review
5. Merge après approbation

**Protection de main :**
- Interdire les push directs sur main
- Obliger les Pull Requests
- Nécessiter des reviews

---

## Aller plus loin

### Commandes avancées

#### Stash (mettre de côté temporairement)

**Situation :** Tu travailles sur `develop` mais tu dois changer de branche rapidement.

```bash
# Mettre de côté les modifications
git stash

# Changer de branche
git checkout main

# ... faire quelque chose ...

# Revenir sur develop
git checkout develop

# Récupérer les modifications
git stash pop
```

**Commandes stash :**
```bash
git stash                # Mettre de côté
git stash list           # Lister les stashs
git stash pop            # Récupérer et supprimer
git stash apply          # Récupérer sans supprimer
git stash drop           # Supprimer
git stash clear          # Tout supprimer
```

#### Rebase (réécrire l'historique)

**Attention :** Uniquement sur tes branches, jamais sur main !

```bash
# Mettre à jour develop avec les commits de main
git checkout develop
git rebase main
```

**Rebase interactif (modifier plusieurs commits) :**
```bash
git rebase -i HEAD~3
```

**Options :**
- `pick` : garder le commit
- `reword` : modifier le message
- `edit` : modifier le contenu
- `squash` : fusionner avec le précédent
- `drop` : supprimer

#### Cherry-pick (copier un commit)

```bash
# Copier un commit d'une autre branche
git cherry-pick a3f5b2c
```

**Exemple :** Tu as fait un commit sur `develop` mais il devrait être sur `main`.

#### Tags (versions)

```bash
# Créer un tag
git tag v1.0.0

# Tag avec message
git tag -a v1.0.0 -m "Version 1.0.0 stable"

# Pousser les tags
git push --tags

# Lister les tags
git tag
```

### Alias Git (raccourcis)

Ajouter à ta config pour gagner du temps :

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --oneline --graph --all'
```

**Utilisation :**
```bash
git st              # = git status
git co develop      # = git checkout develop
git visual          # = git log --oneline --graph --all
```

### Git Hooks (automation)

Les hooks sont des scripts automatiques déclenchés par Git.

**Exemple :** Linter automatique avant commit.

```bash
# Créer le hook
nano .git/hooks/pre-commit
```

**Contenu :**
```bash
#!/bin/sh
npm run lint
```

**Rendre exécutable :**
```bash
chmod +x .git/hooks/pre-commit
```

Maintenant, `npm run lint` s'exécute avant chaque commit.

### Sous-modules (projets dans projets)

```bash
# Ajouter un sous-module
git submodule add https://github.com/user/lib.git libs/lib

# Cloner un projet avec sous-modules
git clone --recursive https://github.com/user/projet.git

# Mettre à jour les sous-modules
git submodule update --remote
```

### Git Flow (workflow avancé)

Structure complète pour projets complexes :

```
main          ← Production
  └─ develop  ← Développement principal
      ├─ feature/login
      ├─ feature/profile
      └─ release/v1.0
           └─ hotfix/critical-bug
```

**Installation :**
```bash
# Linux
sudo apt install git-flow

# macOS
brew install git-flow
```

**Utilisation :**
```bash
git flow init
git flow feature start login
git flow feature finish login
```

### GitHub Actions (CI/CD)

Automatiser les tests et déploiements.

**Exemple : `.github/workflows/test.yml`**
```yaml
name: Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run tests
        run: npm test
```

### GitHub Pages (déploiement gratuit)

Héberger un site statique gratuitement :

1. Va dans **Settings** de ton repo
2. **Pages** dans le menu
3. Source : branche `main`, dossier `/` (ou `/docs`)
4. Save

Ton site sera sur : `https://username.github.io/repo-name`

---

## Ressources et aide

### Documentation officielle

- [Git Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com)
- [Git Book (français)](https://git-scm.com/book/fr/v2)

### Aide intégrée

```bash
git help <commande>
git <commande> --help

# Exemples
git help commit
git push --help
```

### Outils graphiques

**Clients Git GUI :**
- [GitKraken](https://www.gitkraken.com/) (complet, gratuit pour usage perso)
- [GitHub Desktop](https://desktop.github.com/) (simple, officiel)
- [SourceTree](https://www.sourcetreeapp.com/) (avancé, gratuit)
- [Git Cola](https://git-cola.github.io/) (léger, open-source)

**Extensions VS Code :**
- GitLens
- Git Graph
- Git History

### Visualiser Git

**En ligne :**
- [Learn Git Branching](https://learngitbranching.js.org/) (interactif, excellent)
- [Git Visualizer](https://git-school.github.io/visualizing-git/)

### Cheat sheets

```bash
# Télécharger un PDF de référence rapide
wget https://education.github.com/git-cheat-sheet-education.pdf
```

---

## Récapitulatif workflow complet

### Setup initial (une fois)

```bash
# 1. Configuration
git config --global user.name "Ton Nom"
git config --global user.email "ton@email.com"

# 2. SSH
ssh-keygen -t ed25519 -C "ton@email.com"
cat ~/.ssh/id_ed25519.pub
# → Ajouter à GitHub

# 3. Nouveau projet
mkdir mon-projet && cd mon-projet
git init
echo "# Mon Projet" > README.md
git add .
git commit -m "chore: initialiser le projet"

# 4. Lier à GitHub
git remote add origin git@github.com:USERNAME/mon-projet.git
git branch -M main
git push -u origin main

# 5. Créer develop
git checkout -b develop
git push -u origin develop
```

### Workflow quotidien

```bash
# 1. Commencer la journée
git checkout develop
git pull

# 2. Travailler
# ... coder ...

# 3. Commiter régulièrement
git status
git add .
git commit -m "feat: ajouter fonctionnalité X"
git push

# 4. Mettre en production (quand prêt)
git checkout main
git merge develop
git push

# 5. Retourner sur develop
git checkout develop
```

### Commandes les plus utilisées

```bash
git status              # État actuel
git add .               # Ajouter fichiers
git commit -m "..."     # Créer commit
git push                # Envoyer sur GitHub
git pull                # Récupérer de GitHub
git checkout <branche>  # Changer de branche
git log --oneline       # Voir l'historique
git diff                # Voir les modifications
```

---

## Conclusion

### Ce que tu dois retenir

1. **Git ≠ GitHub**
   - Git = outil local
   - GitHub = plateforme en ligne

2. **Les 3 zones**
   - Working directory → Staging → Repository

3. **Workflow develop → main**
   - develop = travail
   - main = production

4. **Commit souvent, petits commits**
   - Messages clairs
   - Convention `type: description`

5. **Branches pour isoler**
   - Jamais coder sur main
   - Toujours tester avant de merger

### Prochaines étapes

1. **Pratique** : Crée un projet test et expérimente
2. **Routine** : Utilise Git quotidiennement
3. **Explore** : Teste les commandes avancées
4. **Automatise** : Configure des alias et hooks
5. **Partage** : Contribue à l'open-source

### En cas de doute

1. `git status` est ton ami
2. Google/ChatGPT avec le message d'erreur exact
3. La documentation Git est excellente
4. Teste sur un repo de test avant le vrai projet

---

**Bon code et bon Git ! 🚀**
