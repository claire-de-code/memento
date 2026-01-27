# Logseq + GitHub — Connecter le plugin Git (Flatpak) via HTTPS + Token

Ce document décrit **le processus complet** pour connecter le **plugin Git de Logseq** à **GitHub** quand SSH est compliqué (cas fréquent sous Flatpak). La solution la plus fiable est :

- **Remote Git en HTTPS**
- Authentification via **Personal Access Token (PAT)**
- Stockage des identifiants avec : `git config --global credential.helper store`

> ⚠️ Note sécurité : `credential.helper store` enregistre le token **en clair** dans `~/.git-credentials` (protégé par les permissions Unix). C’est le compromis “ça marche partout, même sans UI”.

---

## 0) Pré-requis

- Un graph Logseq stocké dans un dossier normal (ex : `~/Documents/logseq`)
- Ce dossier contient un dépôt Git (`.git/`)
- Logseq installé (Flatpak ou autre)

Vérifier que tu es dans le bon dossier :

```bash
cd ~/Documents/logseq
ls -a
```

Tu dois voir un dossier `.git`.

---

## 1) Créer un dépôt Git local (si ce n’est pas déjà fait)

Dans le dossier de ton graph :

```bash
cd ~/Documents/logseq
git init
```

Créer un `.gitignore` minimal (optionnel mais conseillé) :

```bash
nano .gitignore
```

Contenu recommandé :

```gitignore
logseq/bak/
logseq/.recycle/
logseq/.graphs/
.DS_Store
```

Premier commit :

```bash
git add .
git commit -m "initial: logseq graph"
```

---

## 2) Créer le dépôt sur GitHub

Sur GitHub :

1. **New repository**
2. Nom : ex `logseq-notes`
3. **Private** ✅ (recommandé)
4. Ne pas initialiser (pas de README/.gitignore sur GitHub)

Ensuite, GitHub affiche l’URL du repo.

---

## 3) Créer un token (PAT) sur GitHub

### Accès au menu

GitHub → **Settings** → **Developer settings** → **Personal access tokens**

Choisir de préférence :

- **Fine-grained personal access token**

### Configuration recommandée

- **Repository access** : *Only selected repositories*
  - sélectionne uniquement le repo Logseq
- **Permissions** (Repository permissions) :
  - **Contents** → **Read and write**
- **Expiration** : 30 / 90 jours (au choix)

Clique **Generate token**.

✅ Copie le token immédiatement (tu ne le reverras plus).

---

## 4) Passer le remote du repo Logseq en HTTPS

Dans ton repo local :

```bash
cd ~/Documents/logseq
```

Voir le remote actuel :

```bash
git remote -v
```

Changer l’URL pour HTTPS :

```bash
git remote set-url origin https://github.com/TON_USER/TON_REPO.git
```

Re-vérifier :

```bash
git remote -v
```

---

## 5) Définir la branche et l’upstream (si nécessaire)

S’assurer que la branche s’appelle `main` :

```bash
git branch -M main
```

Premier push + création du tracking upstream :

```bash
git push --set-upstream origin main
```

---

## 6) Éviter les prompts dans Logseq (Flatpak) : enregistrer le token

### Problème courant

Le plugin Git dans Logseq (Flatpak) peut échouer avec :

- `ssh-askpass: No such file or directory`
- `could not read Username for 'https://github.com'`

Parce qu’il ne peut pas afficher de prompt interactif.

### Solution

Activer le stockage des identifiants :

```bash
git config --global credential.helper store
```

Ensuite, faire **une fois** un push depuis le terminal (pour que Git enregistre le token) :

```bash
cd ~/Documents/logseq
git push origin main
```

Quand Git demande :

- **Username** : ton identifiant GitHub
- **Password** : colle ton **PAT**

Git sauvegarde alors le token dans :

- `~/.git-credentials`

Après ça, Logseq peut faire `pull/push` sans demander de credentials.

---

## 7) Workflow quotidien (multi-machines)

### Avant d’écrire (sur chaque machine)

```bash
cd ~/Documents/logseq
git pull --rebase origin main
```

Si Git refuse (index sale), commit d’abord :

```bash
git add .
git commit -m "update: $(date '+%F %H:%M')"
```

Puis :

```bash
git pull --rebase origin main
```

### Après ta session Logseq

```bash
git add .
git commit -m "update: $(date '+%F %H:%M')"
git push origin main
```

---

## 8) Installer et utiliser le plugin Git dans Logseq

Dans Logseq :

1. ⚙️ Settings
2. Plugins
3. Marketplace
4. Cherche **Git**
5. Installe

Ensuite, depuis l’UI du plugin :

- Pull (avant d’écrire)
- Commit
- Push

---

## 9) Dépannage rapide

### A) `cannot pull with rebase: You have unstaged changes`

→ Il faut commit ou stash. Recommandé : commit.

```bash
git add .
git commit -m "update: $(date '+%F %H:%M')"
```

### B) `main has no upstream branch`

```bash
git push --set-upstream origin main
```

### C) Le token a expiré / a été révoqué

- Crée un nouveau token
- Remplace l’entrée dans `~/.git-credentials` (ou supprime-la puis refais un push)

Voir le fichier :

```bash
cat ~/.git-credentials
```

Supprimer les credentials (pour repartir propre) :

```bash
rm ~/.git-credentials
```

Puis refaire :

```bash
git push origin main
```

---

## Résumé

La méthode la plus fiable pour Logseq (Flatpak) :

1. GitHub : créer un **PAT** limité au repo Logseq
2. Repo : remote en **HTTPS**
3. Local : `git config --global credential.helper store`
4. Terminal : faire un push une fois pour enregistrer le token
5. Logseq : le plugin Git fonctionne ensuite sans prompts

