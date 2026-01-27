# 📓 Guide Expert Logseq — PKM, Git & Workflow Complet

Guide complet pour maîtriser Logseq comme système de gestion de connaissances avec synchronisation Git.

---

## 📋 Table des matières

1. [Introduction à Logseq](#introduction-à-logseq)
2. [Installation et configuration](#installation-et-configuration)
3. [Concepts fondamentaux](#concepts-fondamentaux)
4. [Synchronisation Git/GitHub](#synchronisation-gitgithub)
5. [Workflow quotidien optimal](#workflow-quotidien-optimal)
6. [Plugins essentiels](#plugins-essentiels)
7. [Organisation avancée](#organisation-avancée)
8. [Dépannage](#dépannage)
9. [Zettelkasten et PKM](#zettelkasten-et-pkm)
10. [Trucs et astuces](#trucs-et-astuces)

---

## Introduction à Logseq

### Qu'est-ce que Logseq ?

**Logseq** est un outil de **Personal Knowledge Management (PKM)** open-source :
- Outliner (organisation hiérarchique par blocs)
- Graph de connaissances bidirectionnel
- Markdown natif + stockage local
- Privacy-first (tes données restent chez toi)

**Philosophie** : Notes liées, pas isolées.

### Logseq vs alternatives

| Critère | Logseq | Obsidian | Notion | Roam Research |
|---------|--------|----------|--------|---------------|
| **Stockage** | Local (Markdown) | Local (Markdown) | Cloud propriétaire | Cloud propriétaire |
| **Prix** | Gratuit | Gratuit (sync payant) | Freemium | $15/mois |
| **Open-source** | Oui | Non | Non | Non |
| **Sync natif** | Non (Git/cloud) | Payant | Inclus | Inclus |
| **Outliner** | Oui | Non | Oui | Oui |
| **Graph** | Oui | Oui | Non | Oui |
| **Offline** | Oui | Oui | Non | Non |

**Pourquoi Logseq ?**
- Contrôle total des données
- Format pérenne (Markdown)
- Gratuit sans limitations
- Extensible (plugins)
- Synchronisation Git robuste

### Cas d'usage

- **PKM** : système Zettelkasten
- **Journal quotidien** : daily notes automatiques
- **Gestion de projets** : TODO, queries
- **Recherche** : littérature review, notes liées
- **Cours/études** : prise de notes structurée
- **Documentation** : wiki personnel

---

## Installation et configuration

### Installation

#### Linux (Flatpak recommandé)

```bash
# EndeavourOS/Arch
flatpak install flathub com.logseq.Logseq

# Lancer
flatpak run com.logseq.Logseq
```

**Avantages Flatpak** :
- Isolation (sandboxing)
- Mises à jour automatiques
- Indépendant de la distro

**Inconvénient** :
- SSH compliqué → solution HTTPS recommandée

#### Linux (AppImage)

```bash
# Télécharger depuis GitHub releases
wget https://github.com/logseq/logseq/releases/download/VERSION/Logseq-linux-x64-VERSION.AppImage

# Rendre exécutable
chmod +x Logseq-linux-x64-VERSION.AppImage

# Lancer
./Logseq-linux-x64-VERSION.AppImage
```

#### Linux (AUR pour Arch/EndeavourOS)

```bash
yay -S logseq-desktop-bin
```

### Premier lancement

1. **Create new graph** ou **Open existing folder**
2. Choisir emplacement (recommandé : `~/Documents/logseq-notes`)
3. Format : **Markdown** (pas org-mode sauf si besoin spécifique)

### Configuration initiale

**Settings (⚙️) → General** :

```
✓ Show brackets around page references
✓ Enable flashcards
✓ Enable journals
✓ Enable all pages
Journal date format: yyyy-MM-dd
Preferred workflow: NOW/LATER (ou TODO/DOING)
```

**Settings → Editor** :

```
✓ Auto-pairing brackets
✓ Spell check
Default home page: journals (ou page spécifique)
```

**Settings → Version control** :

```
Auto-commit: ✓ (optionnel, pratique)
```

### Structure du graph

```
~/Documents/logseq-notes/
├── journals/          # Notes quotidiennes (auto)
│   ├── 2025-01-27.md
│   └── 2025-01-28.md
├── pages/            # Pages permanentes
│   ├── PKM.md
│   ├── Projects.md
│   └── Inbox.md
├── logseq/           # Config Logseq
│   ├── config.edn
│   ├── custom.css
│   └── plugins/
└── assets/           # Médias (images, PDF)
```

**IMPORTANT** : Tout est en Markdown plain text.

---

## Concepts fondamentaux

### Blocs (Blocks)

**Unité atomique** de Logseq = le bloc.

```markdown
- Ceci est un bloc
  - Ceci est un sous-bloc
    - Encore un niveau
```

**Manipulation** :
- `Tab` : indenter (enfant)
- `Shift+Tab` : désindenter (parent)
- `Alt+↑/↓` : déplacer bloc
- `Ctrl+↑/↓` : swap avec voisin

**Block reference** :
- Chaque bloc a un ID unique
- `((` puis taper → chercher bloc
- Référencer n'importe où

### Pages et liens

**Page** = fichier Markdown dans `pages/`.

**Créer lien** :
```markdown
[[Nom de la page]]
```

**Alias** :
```markdown
[[Nom technique|Nom affiché]]
```

**Tags** :
```markdown
#tag ou #[[tag avec espaces]]
```

### Bi-directional links

**Magie de Logseq** : liens bidirectionnels automatiques.

Si `Page A` référence `[[Page B]]` :
- `Page B` affiche "Linked References" vers `Page A`

**Construire réseau de connaissances** sans effort.

### Namespaces

**Hiérarchie** avec `/` :

```markdown
[[Projet/Backend]]
[[Projet/Frontend]]
[[Projet/DevOps]]
```

Logseq crée automatiquement page parent `Projet`.

### Properties

**Métadonnées** sur blocs/pages :

```markdown
- Description du projet
  property:: valeur
  tags:: #projet, #actif
  deadline:: 2025-12-31
```

**Requêtes** peuvent filtrer par properties.

### Queries

**Langage de requête** pour afficher blocs dynamiquement.

**Simple query** :
```clojure
{{query TODO}}
```

**Advanced query** :
```clojure
#+BEGIN_QUERY
{:title "Tâches du projet X"
 :query [:find (pull ?b [*])
         :where
         [?b :block/marker ?m]
         [(contains? #{"TODO" "DOING"} ?m)]
         [?b :block/page ?p]
         [?p :block/name "projet-x"]]}
#+END_QUERY
```

### TODO système

**Markers** :
- `NOW` : en cours
- `LATER` : planifié
- `TODO` : à faire
- `DOING` : en cours (alt)
- `DONE` : terminé
- `WAITING` : en attente
- `CANCELED` : annulé

**Créer TODO** :
```markdown
- TODO Appeler client
  DEADLINE: <2025-01-30>
```

**Cycle** : `Ctrl+Enter` sur bloc.

---

## Synchronisation Git/GitHub

### Pourquoi Git pour Logseq ?

**Avantages** :
- Versionning complet
- Historique de toutes modifications
- Sync multi-machines robuste
- Backup automatique
- Gratuit (GitHub privé illimité)

**Alternatives** :
- Logseq Sync (15€/mois)
- Syncthing (complexe)
- Cloud classique (risque conflits)

### Méthode HTTPS + Token (recommandée Flatpak)

#### Étape 1 : Initialiser Git local

```bash
cd ~/Documents/logseq-notes
git init
```

#### Étape 2 : Créer .gitignore

```bash
nano .gitignore
```

**Contenu recommandé** :
```gitignore
# Logseq internals
logseq/bak/
logseq/.recycle/
logseq/graphs-txid.edn
logseq/metadata.edn

# Caches
.cache/
.DS_Store
Thumbs.db

# Locks
.lock

# Optionnel : exclure plugins (si volumineux)
# logseq/plugins/
```

#### Étape 3 : Premier commit

```bash
git add .
git commit -m "chore: init logseq graph"
```

#### Étape 4 : Créer repo GitHub

1. GitHub → New repository
2. Nom : `logseq-notes`
3. **Private** ✓
4. Pas de README/gitignore

#### Étape 5 : Créer Personal Access Token

**GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens**

**Configuration** :
- Repository access : Only select repositories → logseq-notes
- Permissions :
  - Contents : Read and write ✓
  - Metadata : Read-only (auto)
- Expiration : 90 jours (renouveler régulièrement)

**Copier token immédiatement.**

#### Étape 6 : Configurer remote HTTPS

```bash
git remote add origin https://github.com/USERNAME/logseq-notes.git
git branch -M main
```

#### Étape 7 : Stocker credentials

```bash
git config --global credential.helper store
```

**Note sécurité** : Token stocké en clair dans `~/.git-credentials`. Permissions `600`.

#### Étape 8 : Premier push

```bash
git push -u origin main
```

**Prompts** :
- Username : `USERNAME`
- Password : **coller token**

Git enregistre dans `~/.git-credentials`.

#### Étape 9 : Vérifier

```bash
cat ~/.git-credentials
```

**Sortie** :
```
https://USERNAME:ghp_XXXXXXXXXX@github.com
```

### Plugin Git dans Logseq

#### Installation

Logseq → Settings → Plugins → Marketplace → **Git**

#### Configuration plugin

Settings du plugin :
```
Auto pull: ✓ (au lancement)
Auto push: ✓ (après commit)
Auto commit interval: 30 minutes
Commit message template: auto: {date}
```

#### Utilisation quotidienne

**Workflow** :
1. Lancer Logseq → Auto-pull
2. Travailler normalement
3. Plugin commit auto toutes les 30 min
4. Fermer Logseq → Auto-push

**Manuellement** :
- `Ctrl+Shift+G` : Pull
- `Ctrl+Shift+C` : Commit
- `Ctrl+Shift+P` : Push

### Multi-machines

**Machine A (premier setup)** :
```bash
cd ~/Documents/logseq-notes
git push origin main
```

**Machine B (clone)** :
```bash
cd ~/Documents
git clone https://github.com/USERNAME/logseq-notes.git
cd logseq-notes

# Configurer credentials
git config credential.helper store
git pull  # Entrer token une fois
```

**Workflow quotidien chaque machine** :
```bash
# AVANT Logseq
cd ~/Documents/logseq-notes
git pull --rebase origin main

# APRÈS Logseq
git add .
git commit -m "update: $(date +%F)"
git push origin main
```

**Automatiser avec alias** :
```bash
# ~/.bashrc
alias logseq-sync='cd ~/Documents/logseq-notes && git pull --rebase origin main && flatpak run com.logseq.Logseq && git add . && git commit -m "update: $(date +%F_%H:%M)" && git push origin main'
```

### Résoudre conflits

**Scénario** : modifications simultanées sur 2 machines.

**Symptôme** :
```
CONFLICT (content): Merge conflict in journals/2025-01-27.md
```

**Solution** :

1. **Ouvrir fichier conflit** :
```bash
nano journals/2025-01-27.md
```

2. **Chercher markers** :
```markdown
<<<<<<< HEAD
- Note version locale
=======
- Note version distante
>>>>>>> origin/main
```

3. **Merger manuellement** (garder les deux ou choisir) :
```markdown
- Note version locale
- Note version distante
```

4. **Résoudre** :
```bash
git add journals/2025-01-27.md
git rebase --continue
git push origin main
```

**Prévention** :
- Toujours pull avant de travailler
- Auto-commit fréquent
- Éviter éditer même fichier simultanément

---

## Workflow quotidien optimal

### Morning routine

```
1. Lancer Logseq (auto-pull via plugin)
2. Ouvrir journal du jour (auto-créé)
3. Daily review :
   - Bloc "Objectifs du jour"
   - Query TODO prioritaires
   - Relecture journal veille
```

**Template journal** :

```markdown
- [[2025-01-27]]
  - ## Objectifs du jour
    - TODO [[Projet X]] Terminer feature Y
    - TODO Lire article Z
  - ## Notes
  - ## Apprentissages
  - ## Review
    - {{query (and (todo NOW LATER) (not (page "Archive")))}}
```

### Capture rapide

**Principe** : noter immédiatement, organiser plus tard.

**Méthode** :
1. `Ctrl+K` : Quick capture
2. Taper note dans journal
3. Plus tard : refactor vers pages permanentes

### Processing inbox

**Page Inbox** :
```markdown
- [[Inbox]]
  - Idées en vrac
  - Liens à trier
  - Notes temporaires
```

**Weekly review** :
- Parcourir Inbox
- Transformer en pages permanentes
- Lier au graph existant
- Vider Inbox

### Linking strategy

**Règle** : toujours lier nouvelles notes.

**Exemple** :
```markdown
- Note sur [[Zettelkasten]]
  - Inspiré par [[Niklas Lumann]]
  - Complémente [[PKM]]
  - Utilisé dans [[Projet/Recherche]]
```

**Graph exploratoire** :
- Cliquer icône graph (en haut à droite)
- Visualiser connexions
- Découvrir liens inattendus

### Evening routine

```
1. Review journal du jour
2. Ajouter bloc "Gratitude" ou "Highlights"
3. Planifier lendemain
4. Commit + push (auto ou manuel)
```

---

## Plugins essentiels

### Plugin Git

**Déjà couvert ci-dessus.**

**Alternatives** :
- Logseq Sync (payant)
- Git via terminal uniquement

### Tabs

**Permet** : ouvrir pages dans onglets (comme navigateur).

**Installation** : Marketplace → Tabs

**Usage** :
- `Ctrl+T` : nouvel onglet
- `Ctrl+W` : fermer onglet
- Glisser-déposer pour réorganiser

### Query Table

**Afficher résultats queries en tableau.**

**Exemple** :
```clojure
#+BEGIN_QUERY
{:title "Tâches par projet"
 :query [:find ?task ?project
         :where
         [?b :block/marker "TODO"]
         [?b :block/content ?task]
         [?b :block/refs ?p]
         [?p :block/name ?project]]}
#+END_QUERY
```

Rendu tabulaire automatique.

### Page Preview

**Prévisualiser pages** au survol lien.

Gain de temps énorme.

### Flashcards

**Intégré** dans Logseq (activer dans Settings).

**Créer carte** :
```markdown
- Question ? #card
  - Réponse
```

**Réviser** : `/` → Flashcards

**Algorithme** : spaced repetition.

### PDF Highlights

**Annoter PDFs** directement dans Logseq.

**Workflow** :
1. Drag-drop PDF dans assets/
2. Cliquer PDF
3. Sélectionner texte → highlight
4. Notes liées automatiquement

### Pomodoro Timer

**Technique Pomodoro** intégrée.

**Usage** :
```markdown
- TODO Écrire article
  {{pomodoro 25}}
```

Clique → démarre timer.

### Templates

**Créer templates** réutilisables.

**Définir** :
```markdown
- [[Templates/Réunion]]
  template:: Réunion
  - Date : {{date}}
  - Participants :
  - Objectif :
  - Notes :
  - Actions :
```

**Utiliser** :
```markdown
- TODO Réunion client
  template:: Réunion
```

`Ctrl+Enter` → remplit template.

---

## Organisation avancée

### Système Zettelkasten

**Principe** : notes atomiques liées.

**Structure** :
```
1. Note Fleeting (journal) → idées brutes
2. Note Literature (pages) → résumés sources
3. Note Permanent (pages) → concepts propres
```

**Exemple** :
```markdown
- [[Zettelkasten Method]]
  - Type : #Permanent
  - Sources : [[How to Take Smart Notes]], [[Niklas Lumann]]
  - ## Définition
    - Système de notes atomiques interliées
  - ## Avantages
    - Favorise [[Pensée émergente]]
    - Connexions [[Sérendipité]]
  - ## Implémentation Logseq
    - Blocs = notes atomiques
    - Liens = connexions
    - Graph = réseau
```

### MOC (Map of Content)

**Page index** regroupant notes thème.

**Exemple** :
```markdown
- [[MOC/Développement]]
  - ## Langages
    - [[Python]]
    - [[JavaScript]]
    - [[Rust]]
  - ## Concepts
    - [[Design Patterns]]
    - [[Architecture]]
  - ## Projets
    - [[Projet/API Backend]]
```

### PARA Method

**Projects, Areas, Resources, Archives**

```
pages/
├── 1-Projects/      # Objectifs court terme
├── 2-Areas/         # Responsabilités long terme
├── 3-Resources/     # Références
└── 4-Archives/      # Terminé/inactif
```

**Namespaces Logseq** :
```markdown
[[1-Projects/Site Web]]
[[2-Areas/PKM]]
[[3-Resources/Logseq Docs]]
[[4-Archives/Ancien Projet]]
```

### Properties avancées

**Custom properties** pour filtrage.

**Exemple système GTD** :
```markdown
- TODO Appeler client
  context:: #bureau
  energy:: high
  time:: 30m
  project:: [[Projet X]]
```

**Query par context** :
```clojure
{{query (property context #bureau)}}
```

### Hiérarchies pages

**Parent-child** avec namespaces :

```markdown
[[Projet]]
  [[Projet/Backend]]
    [[Projet/Backend/API]]
    [[Projet/Backend/Database]]
  [[Projet/Frontend]]
```

Logseq crée breadcrumb automatique.

---

## Dépannage

### Graph ne se synchronise pas

**Vérifier** :
```bash
cd ~/Documents/logseq-notes
git status
```

**Si uncommitted changes** :
```bash
git add .
git commit -m "fix: manual sync"
git push origin main
```

**Si behind origin** :
```bash
git pull --rebase origin main
```

### Plugin Git erreurs

**`could not read Username`**

**Cause** : credentials non stockées.

**Solution** :
```bash
git config credential.helper store
git push  # Entrer token manuellement
```

**`Permission denied (publickey)`**

**Cause** : tentative SSH (ne marche pas Flatpak).

**Solution** : passer en HTTPS (voir section sync).

### Token expiré

**Symptôme** : push/pull échouent.

**Solution** :
1. Créer nouveau token GitHub
2. Éditer `~/.git-credentials`
3. Remplacer ancien token par nouveau

```bash
nano ~/.git-credentials
```

### Conflit persistent

**Dernier recours** :
```bash
# Backup local
cp -r ~/Documents/logseq-notes ~/logseq-backup

# Reset hard à origin
git fetch origin
git reset --hard origin/main

# Récupérer changements locaux si nécessaire
# (merger manuellement depuis backup)
```

### Logseq lent

**Causes possibles** :
- Graph trop gros (>10k blocs)
- Trop de plugins
- Index corrompu

**Solutions** :
```
1. Settings → Advanced → Re-index
2. Désactiver plugins inutilisés
3. Archiver vieilles notes
4. Vider cache navigateur (Electron)
```

### Flatpak permissions

**Si accès fichiers bloqué** :

```bash
# Autoriser accès home
flatpak override --user com.logseq.Logseq --filesystem=home

# Ou spécifique
flatpak override --user com.logseq.Logseq --filesystem=~/Documents/logseq-notes
```

---

## Zettelkasten et PKM

### Principes Zettelkasten

1. **Atomicité** : une idée = un bloc
2. **Autonomie** : bloc compréhensible seul
3. **Linking** : toujours connecter
4. **Propres mots** : pas de copier-coller
5. **Références** : citer sources

### Workflow Zettelkasten dans Logseq

**Capture** (Fleeting) :
```markdown
- [[2025-01-27]]
  - Idée : utiliser Git pour sync Logseq #fleeting
```

**Élaboration** (Literature) :
```markdown
- [[Logseq Git Sync Article]]
  - Source : https://...
  - ## Notes
    - Git permet version control
    - HTTPS + token évite SSH
```

**Permanent note** :
```markdown
- [[Git Sync for PKM Tools]]
  - Related : [[Version Control]], [[Logseq]], [[PKM Best Practices]]
  - ## Concept
    - Git adapté PKM car Markdown plain text
    - Permet multi-machine robuste
  - ## Implémentation
    - HTTPS + PAT pour auth simple
    - .gitignore pour exclure caches
```

### Progressive summarization

**Niveaux surlignage** :

```markdown
- Layer 1 : texte brut
  - Layer 2 : **bold** passages importants
    - Layer 3 : `highlight` essence
      - Layer 4 : [[Link]] concepts clés
```

### Evergreen notes

**Notes pérennes** qui évoluent.

**Caractéristiques** :
- Titre = assertion (pas question)
- Densément liées
- Mises à jour régulièrement
- Autonomes

**Exemple** :
```markdown
- [[Version Control Enables Collaborative Knowledge]]
  - Mis à jour : 2025-01-27
  - ## Argument
    - Git permet tracking précis changements
    - Facilite merge connaissances multiples sources
    - Historique = audit trail pensée
  - ## Liens
    - [[Git]], [[PKM]], [[Distributed Systems]]
  - ## Sources
    - [[Building a Second Brain]]
    - Expérience personnelle
```

---

## Trucs et astuces

### Raccourcis clavier essentiels

```
Ctrl+K     : Quick capture
Ctrl+O     : Recherche page/bloc
Ctrl+Shift+K : Graph global
Ctrl+Shift+P : Command palette
Tab        : Indenter
Shift+Tab  : Désindenter
Ctrl+Enter : Cycle TODO
//         : Date picker
[[         : Créer lien
((         : Référence bloc
{{         : Slash commands
```

### Slash commands utiles

```
/TODO      : Créer tâche
/NOW       : Tâche urgente
/template  : Insérer template
/query     : Créer query
/draw      : Whiteboard
/calculator: Calculatrice
/youtube   : Embed video
```

### Custom CSS

**Personnaliser apparence** :

```bash
nano ~/Documents/logseq-notes/logseq/custom.css
```

**Exemples** :

```css
/* Largeur maximale contenu */
.cp__sidebar-main-content {
  max-width: 900px;
  margin: 0 auto;
}

/* Police journal */
.journal {
  font-family: 'JetBrains Mono', monospace;
}

/* Highlight blocs référencés */
.block-ref {
  background-color: rgba(255, 212, 0, 0.1);
  border-left: 3px solid #ffd400;
  padding-left: 8px;
}
```

### Queries avancées

**TODOs avec deadline proche** :
```clojure
#+BEGIN_QUERY
{:title "Urgent (< 3 jours)"
 :query [:find (pull ?b [*])
         :where
         [?b :block/marker ?m]
         [(contains? #{"TODO" "DOING"} ?m)]
         [?b :block/deadline ?d]
         [(< ?d 20250130)]]}
#+END_QUERY
```

**Pages modifiées derniers 7 jours** :
```clojure
{{query (and (page-property last-modified) (between [[7 days ago]] [[today]]))}}
```

### Backlinks automatiques

**Utiliser références implicites** :

```markdown
- [[Python]] est un langage
  - Utilisé dans [[Machine Learning]]
    - Library principale : [[TensorFlow]]
```

Chaque page affiche automatiquement mentions.

### Export

**Formats supportés** :
- Markdown (natif)
- OPML (outline)
- JSON (graph complet)

**Export graph** :
```
Settings → Export graph → Choose format
```

### Backup strategy

**Git = backup primaire.**

**Backup additionnel** :

```bash
# Script backup local
#!/bin/bash
rsync -av ~/Documents/logseq-notes/ ~/Backups/logseq-$(date +%F)/

# Ou cloud
rclone sync ~/Documents/logseq-notes/ gdrive:logseq-backup
```

---

## Ressources

### Documentation officielle

- **Docs** : https://docs.logseq.com/
- **GitHub** : https://github.com/logseq/logseq
- **Discord** : Communauté active

### Communauté

- **Forum** : https://discuss.logseq.com/
- **Reddit** : r/logseq
- **YouTube** : nombreux tutoriels

### Lectures PKM

- *How to Take Smart Notes* (Sönke Ahrens)
- *Building a Second Brain* (Tiago Forte)
- *The Zettelkasten Method* (Sönke Ahrens)

### Plugins recommandés

- **Git** : sync essentiel
- **Tabs** : navigation améliorée
- **Query Table** : visualisation
- **Awesome UI** : améliorations interface
- **Pomodoro** : gestion temps

---

## Checklist démarrage

```
Installation :
[ ] Installer Logseq (Flatpak/AppImage/AUR)
[ ] Créer graph (~/Documents/logseq-notes)
[ ] Configurer Settings (Markdown, journals)

Git :
[ ] git init
[ ] Créer .gitignore
[ ] Premier commit
[ ] Créer repo GitHub privé
[ ] Générer PAT
[ ] Configurer remote HTTPS
[ ] credential.helper store
[ ] Premier push
[ ] Installer plugin Git Logseq

Workflow :
[ ] Template journal quotidien
[ ] Page Inbox
[ ] MOC principale
[ ] Premiers liens

Pratique :
[ ] Tester sync multi-machines
[ ] Configurer plugins essentiels
[ ] Personnaliser CSS
[ ] Créer queries utiles
```

---

## Conclusion

**Logseq + Git** = système PKM puissant, gratuit, et pérenne.

**Clés succès** :
- Sync régulier (automatisé)
- Linking systématique
- Review hebdomadaire
- Backup robuste

**Commencer simple** :
1. Journal quotidien
2. Quelques pages
3. Lier naturellement
4. Graph émerge organiquement

Le système grandit avec toi.
