# 🧠 Mémento Vim — Guide IDE sans plugins

## 📋 Table des matières

1. [Modes](#modes)
2. [Déplacements](#déplacements)
3. [Édition](#édition)
4. [Sélection visuelle](#sélection-visuelle)
5. [Recherche](#recherche)
6. [Remplacement](#remplacement)
7. [Fichiers et buffers](#fichiers-et-buffers)
8. [Fenêtres (splits)](#fenêtres-splits)
9. [Indentation](#indentation)
10. [Macros](#macros)
11. [Explorateur de fichiers](#explorateur-de-fichiers-netrw)
12. [Build et compilation](#build-et-compilation)
13. [Autocomplétion](#autocomplétion-native)
14. [Raccourcis personnalisés](#raccourcis-personnalisés-de-ton-vimrc)
15. [Sessions](#sessions-sauvegarder-ton-environnement)
16. [Astuces avancées](#astuces-avancées)
17. [Cheat sheet rapide](#cheat-sheet-rapide)

---

## Modes

| Commande | Action |
|----------|--------|
| `i` | Insertion **avant** le curseur |
| `I` | Insertion **début de ligne** |
| `a` | Insertion **après** le curseur |
| `A` | Insertion **fin de ligne** |
| `o` | Nouvelle ligne **en dessous** |
| `O` | Nouvelle ligne **au-dessus** |
| `Esc` | Retour au mode normal |
| `v` | Sélection visuelle (caractères) |
| `V` | Sélection visuelle (lignes entières) |
| `Ctrl+v` | Sélection en bloc (colonnes) |
| `:` | Mode commande |

**Astuce :** Le mode normal est le mode par défaut. Tu passes la majorité de ton temps ici.

---

## Déplacements

### Déplacements de base
| Commande | Action |
|----------|--------|
| `h` `j` `k` `l` | Gauche / Bas / Haut / Droite |
| `w` | Début du mot suivant |
| `b` | Début du mot précédent |
| `e` | Fin du mot |
| `0` | Début de ligne (colonne 0) |
| `^` | Premier caractère non-blanc |
| `$` | Fin de ligne |

### Déplacements dans le fichier
| Commande | Action |
|----------|--------|
| `gg` | Première ligne du fichier |
| `G` | Dernière ligne du fichier |
| `50G` ou `:50` | Aller à la ligne 50 |
| `Ctrl+d` | Descendre d'une demi-page |
| `Ctrl+u` | Monter d'une demi-page |
| `Ctrl+f` | Page suivante (forward) |
| `Ctrl+b` | Page précédente (backward) |
| `zz` | Centrer la ligne courante à l'écran |
| `zt` | Ligne courante en haut de l'écran |
| `zb` | Ligne courante en bas de l'écran |

### Déplacements par recherche
| Commande | Action |
|----------|--------|
| `f{char}` | Aller au prochain `{char}` sur la ligne |
| `F{char}` | Aller au précédent `{char}` sur la ligne |
| `t{char}` | Aller juste avant le prochain `{char}` |
| `T{char}` | Aller juste après le précédent `{char}` |
| `;` | Répéter le dernier f/F/t/T |
| `,` | Répéter dans l'autre sens |

**Exemple :** Sur la ligne `const result = calculate(x, y);`  
- `fa` → saute au `a` de `calculate`
- `f(` → saute à la parenthèse ouvrante

---

## Édition

### Suppression
| Commande | Action |
|----------|--------|
| `x` | Supprimer le caractère sous le curseur |
| `X` | Supprimer le caractère avant le curseur |
| `dd` | Supprimer la ligne entière |
| `D` | Supprimer jusqu'à la fin de ligne |
| `dw` | Supprimer le mot |
| `d$` | Supprimer jusqu'à la fin de ligne (= `D`) |
| `d0` | Supprimer jusqu'au début de ligne |
| `dgg` | Supprimer jusqu'au début du fichier |
| `dG` | Supprimer jusqu'à la fin du fichier |

### Copier (yank)
| Commande | Action |
|----------|--------|
| `yy` | Copier la ligne |
| `yw` | Copier le mot |
| `y$` | Copier jusqu'à la fin de ligne |
| `ygg` | Copier jusqu'au début du fichier |
| `yG` | Copier jusqu'à la fin du fichier |

### Coller
| Commande | Action |
|----------|--------|
| `p` | Coller après le curseur/ligne |
| `P` | Coller avant le curseur/ligne |

### Changer (change = supprimer + mode insertion)
| Commande | Action |
|----------|--------|
| `cw` | Changer le mot |
| `cc` | Changer la ligne entière |
| `C` | Changer jusqu'à la fin de ligne |
| `c$` | Changer jusqu'à la fin de ligne (= `C`) |

### Undo / Redo
| Commande | Action |
|----------|--------|
| `u` | Annuler (undo) |
| `Ctrl+r` | Rétablir (redo) |
| `.` | Répéter la dernière action |

**Astuce :** Le `.` est extrêmement puissant. Exemple : `dd` puis `.` `.` `.` supprime 4 lignes.

---

## Sélection visuelle

1. Entrer en mode visuel : `v`, `V`, ou `Ctrl+v`
2. Sélectionner avec les mouvements (`hjkl`, `w`, `$`, etc.)
3. Appliquer une action :

| Commande | Action |
|----------|--------|
| `y` | Copier la sélection |
| `d` | Couper la sélection |
| `c` | Changer la sélection (mode insertion) |
| `>` | Indenter vers la droite |
| `<` | Désindenter vers la gauche |
| `=` | Auto-indenter (reformater) |
| `u` | Mettre en minuscules |
| `U` | Mettre en MAJUSCULES |
| `gv` | Re-sélectionner la dernière sélection |

**Exemple (mode bloc Ctrl+v) :**
```
1. const x = 10;
2. const y = 20;
3. const z = 30;
```
- Place le curseur sur le `c` de ligne 1
- `Ctrl+v` puis `jj` (sélectionne 3 lignes en colonne)
- `I// ` puis `Esc` → commente les 3 lignes

---

## Recherche

| Commande | Action |
|----------|--------|
| `/mot` | Chercher `mot` vers le bas |
| `?mot` | Chercher `mot` vers le haut |
| `n` | Occurrence suivante |
| `N` | Occurrence précédente |
| `*` | Chercher le mot sous le curseur (vers le bas) |
| `#` | Chercher le mot sous le curseur (vers le haut) |
| `:nohlsearch` ou `Esc Esc` | Enlever le surlignage |

**Regex :** Vim supporte les expressions régulières.
- `/function.*()` → cherche "function" suivi de n'importe quoi puis "()"

---

## Remplacement

### Syntaxe de base
```vim
:[range]s/ancien/nouveau/[flags]
```

| Range | Signification |
|-------|---------------|
| `%` | Tout le fichier |
| `.` | Ligne courante |
| `1,10` | Lignes 1 à 10 |
| `'<,'>` | Sélection visuelle (automatique) |

| Flag | Signification |
|------|---------------|
| `g` | Toutes les occurrences sur la ligne |
| `c` | Demande confirmation |
| `i` | Insensible à la casse |

### Exemples
```vim
:%s/foo/bar/g           " Remplacer tous les "foo" par "bar"
:%s/foo/bar/gc          " Idem avec confirmation
:1,10s/old/new/g        " Lignes 1 à 10 uniquement
:'<,'>s/var/let/g       " Dans la sélection visuelle
```

**Astuce :** En mode visuel, sélectionne du texte puis tape `:` → Vim insère automatiquement `:'<,'>`

---

## Fichiers et buffers

### Gestion de fichiers
| Commande | Action |
|----------|--------|
| `:w` | Sauvegarder |
| `:w fichier.txt` | Sauvegarder sous un autre nom |
| `:q` | Quitter |
| `:q!` | Quitter sans sauvegarder |
| `:wq` ou `:x` | Sauvegarder et quitter |
| `:e fichier.txt` | Ouvrir/éditer un fichier |
| `:r fichier.txt` | Insérer le contenu d'un fichier |

### Buffers (fichiers ouverts en mémoire)
| Commande | Action |
|----------|--------|
| `:ls` ou `:buffers` | Liste des buffers |
| `:b 2` | Aller au buffer numéro 2 |
| `:bn` | Buffer suivant |
| `:bp` | Buffer précédent |
| `:bd` | Fermer le buffer actuel |
| `:bd 3` | Fermer le buffer 3 |

**Dans ton .vimrc :**
- `Tab` → buffer suivant
- `Shift+Tab` → buffer précédent

---

## Fenêtres (splits)

### Créer des splits
| Commande | Action |
|----------|--------|
| `:split` ou `:sp` | Split horizontal |
| `:vsplit` ou `:vsp` | Split vertical |
| `:sp fichier.txt` | Split horizontal + ouvrir fichier |

**Dans ton .vimrc :**
- `Space + h` → split horizontal
- `Space + v` → split vertical

### Navigation entre fenêtres
| Commande | Action |
|----------|--------|
| `Ctrl+w h` | Fenêtre de gauche |
| `Ctrl+w j` | Fenêtre du bas |
| `Ctrl+w k` | Fenêtre du haut |
| `Ctrl+w l` | Fenêtre de droite |
| `Ctrl+w w` | Fenêtre suivante (cycle) |

**Dans ton .vimrc :**
- `Ctrl+h/j/k/l` → navigation directe

### Gestion des fenêtres
| Commande | Action |
|----------|--------|
| `Ctrl+w q` | Fermer la fenêtre courante |
| `Ctrl+w =` | Égaliser les tailles |
| `Ctrl+w _` | Maximiser hauteur |
| `Ctrl+w \|` | Maximiser largeur |
| `Ctrl+w r` | Rotation des fenêtres |

---

## Indentation

| Commande | Action |
|----------|--------|
| `>>` | Indenter la ligne vers la droite |
| `<<` | Désindenter la ligne vers la gauche |
| `5>>` | Indenter 5 lignes |
| `>%` | Indenter un bloc (curseur sur `{`) |
| `=%` | Auto-indenter un bloc |
| `gg=G` | Reformater tout le fichier |
| `=G` | Reformater jusqu'à la fin du fichier |

**En mode visuel :**
- Sélectionne des lignes avec `V`
- Tape `>` ou `<` pour indenter/désindenter
- Tape `.` pour répéter

---

## Macros

Les macros permettent d'enregistrer une séquence de commandes et de la rejouer.

| Commande | Action |
|----------|--------|
| `qa` | Commencer l'enregistrement dans le registre `a` |
| `q` | Arrêter l'enregistrement |
| `@a` | Rejouer la macro `a` |
| `@@` | Rejouer la dernière macro |
| `10@a` | Rejouer la macro `a` 10 fois |

**Exemple :** Ajouter `;` à la fin de 10 lignes
1. Place le curseur sur la première ligne
2. `qa` (commence l'enregistrement)
3. `A;<Esc>` (ajoute `;` en fin de ligne)
4. `j` (descend d'une ligne)
5. `q` (arrête l'enregistrement)
6. `9@a` (rejoue 9 fois → total 10 lignes)

---

## Explorateur de fichiers (netrw)

Vim inclut **netrw**, un explorateur de fichiers intégré (pas de plugin nécessaire).

### Ouvrir netrw
| Commande | Action |
|----------|--------|
| `:Ex` ou `:Explore` | Explorateur dans la fenêtre courante |
| `:Vexplore` | Explorateur en split vertical |
| `vim .` | Ouvrir Vim dans un dossier |

**Dans ton .vimrc :**
- `Space + e` → ouvre l'explorateur en sidebar à gauche

### Navigation dans netrw
| Commande | Action |
|----------|--------|
| `Enter` | Ouvrir fichier / entrer dans dossier |
| `-` | Remonter au dossier parent |
| `gh` | Afficher/masquer fichiers cachés |
| `%` | Créer un nouveau fichier |
| `d` | Créer un dossier |
| `D` | Supprimer |
| `R` | Renommer |
| `i` | Changer le style d'affichage |

**Configuration dans ton .vimrc :**
```vim
let g:netrw_banner = 0        " Pas de bannière
let g:netrw_liststyle = 3    " Vue en arbre
let g:netrw_winsize = 25     " Largeur 25%
```

---

## Build et compilation

Vim peut lancer des commandes de build et afficher les erreurs dans un panneau (quickfix).

### Configuration
Dans ton `.vimrc`, définis la commande de build :
```vim
set makeprg=npm\ run\ build     " JavaScript
set makeprg=pytest              " Python
set makeprg=make                " C/C++
set makeprg=cargo\ build        " Rust
```

### Commandes
| Commande | Action |
|----------|--------|
| `:make` | Lancer le build |
| `:copen` | Ouvrir le panneau d'erreurs |
| `:cclose` | Fermer le panneau d'erreurs |
| `:cnext` | Erreur suivante |
| `:cprevious` | Erreur précédente |
| `:cfirst` | Première erreur |
| `:clast` | Dernière erreur |

**Dans ton .vimrc :**
- `Space + m` → sauvegarde + make
- `Space + c` → ouvrir quickfix
- `Space + n` → erreur suivante
- `Space + p` → erreur précédente

### Exemple de workflow
1. Édite ton code
2. `Space + m` → lance le build
3. Si erreurs : `Space + c` → ouvre le panneau
4. `Enter` sur une erreur → saute au fichier/ligne
5. Corrige l'erreur
6. `Space + m` → rebuild

---

## Autocomplétion native

Vim a une autocomplétion puissante **sans plugin**.

### En mode insertion
| Commande | Action |
|----------|--------|
| `Ctrl+n` | Mot suivant (du buffer ou projet) |
| `Ctrl+p` | Mot précédent |
| `Ctrl+x Ctrl+f` | Compléter un chemin de fichier |
| `Ctrl+x Ctrl+l` | Compléter une ligne entière |
| `Ctrl+x Ctrl+o` | Omni-completion (selon langage) |

**Exemple :**
```javascript
const userName = "John";
const user  // Tape Ctrl+n → suggère "userName"
```

### Navigation dans le menu
| Commande | Action |
|----------|--------|
| `Ctrl+n` | Suggestion suivante |
| `Ctrl+p` | Suggestion précédente |
| `Ctrl+y` | Accepter la sélection |
| `Ctrl+e` | Annuler et revenir au texte initial |

---

## Raccourcis personnalisés de ton .vimrc

Voici les raccourcis spécifiques configurés dans ton `.vimrc` :

### Généraux
| Raccourci | Action |
|-----------|--------|
| `Space + w` | Sauvegarder |
| `Space + q` | Quitter |
| `Space + x` | Sauvegarder et quitter |

### Buffers
| Raccourci | Action |
|-----------|--------|
| `Tab` | Buffer suivant |
| `Shift + Tab` | Buffer précédent |
| `Space + bd` | Fermer le buffer |

### Recherche
| Raccourci | Action |
|-----------|--------|
| `Esc Esc` | Enlever le surlignage de recherche |

### Fenêtres
| Raccourci | Action |
|-----------|--------|
| `Space + v` | Split vertical |
| `Space + h` | Split horizontal |
| `Ctrl + h/j/k/l` | Naviguer entre fenêtres |

### Explorateur
| Raccourci | Action |
|-----------|--------|
| `Space + e` | Ouvrir explorateur (sidebar gauche) |

### Build
| Raccourci | Action |
|-----------|--------|
| `Space + m` | Sauvegarder + make |
| `Space + c` | Ouvrir quickfix |
| `Space + n` | Erreur suivante |
| `Space + p` | Erreur précédente |
| `Space + cc` | Fermer quickfix |

### Utilitaires
| Raccourci | Action |
|-----------|--------|
| `Space + i` | Afficher position curseur |
| `Space + t` | Supprimer espaces en fin de ligne |

---

## Sessions (sauvegarder ton environnement)

Les sessions permettent de sauvegarder l'état complet de Vim (buffers, splits, position du curseur).

### Créer une session
```vim
:mksession! .vim.session
```

### Charger une session
```bash
vim -S .vim.session
```

Ou depuis Vim :
```vim
:source .vim.session
```

**Workflow projet :**
1. Ouvre tous tes fichiers, arrange tes splits
2. `:mksession! .vim.session`
3. La prochaine fois : `vim -S .vim.session`

---

## Astuces avancées

### Text objects (objets de texte)

Les "text objects" permettent de manipuler des blocs de texte.

| Commande | Action |
|----------|--------|
| `ciw` | Changer le mot sous le curseur (change inner word) |
| `caw` | Changer le mot + espace après (change a word) |
| `ci"` | Changer dans les guillemets `"..."` |
| `ci'` | Changer dans les apostrophes `'...'` |
| `ci(` ou `cib` | Changer dans les parenthèses `(...)` |
| `ci{` ou `ciB` | Changer dans les accolades `{...}` |
| `ci[` | Changer dans les crochets `[...]` |
| `cit` | Changer dans une balise HTML `<tag>...</tag>` |
| `das` | Supprimer une phrase (delete a sentence) |
| `dap` | Supprimer un paragraphe (delete a paragraph) |

**Remplace `c` par :**
- `d` pour supprimer
- `y` pour copier
- `v` pour sélectionner

**Exemple :** Sur `const name = "John Doe";`
- Curseur sur `John` → `ci"` → efface `John Doe` et passe en mode insertion

### Incrémenter/décrémenter
| Commande | Action |
|----------|--------|
| `Ctrl+a` | Incrémenter le nombre sous le curseur |
| `Ctrl+x` | Décrémenter le nombre sous le curseur |

**Exemple :** Sur `let count = 5;`
- Curseur sur `5` → `Ctrl+a` → devient `6`

### Recherche et remplacement avancé

#### Recherche multi-fichiers
```vim
:vimgrep /pattern/ **/*.js
:copen
```
- Cherche `pattern` dans tous les `.js` du projet
- `:copen` affiche les résultats
- `Enter` sur un résultat pour ouvrir le fichier

#### Recherche incrémentale
```vim
:set incsearch
```
Active la recherche en temps réel pendant la frappe.

### Marks (marques)

Les marks permettent de sauvegarder des positions dans le fichier.

| Commande | Action |
|----------|--------|
| `ma` | Créer une mark `a` à la position courante |
| `` `a `` | Retourner à la mark `a` (position exacte) |
| `'a` | Retourner à la ligne de la mark `a` |
| `:marks` | Lister toutes les marks |

**Marks automatiques :**
- `` `. `` → dernière modification
- `` `` `` → dernière position avant saut
- `''` → dernière ligne avant saut

### Registres

Vim a 26 registres nommés (`a-z`) pour stocker du texte.

| Commande | Action |
|----------|--------|
| `"ayy` | Copier la ligne dans le registre `a` |
| `"ap` | Coller depuis le registre `a` |
| `:reg` | Voir tous les registres |

**Registres spéciaux :**
- `"+` → presse-papiers système (copier)
- `"*` → sélection X11 (Linux)
- `"0` → dernier yank
- `".` → dernier texte inséré

### Commandes shell

Exécuter des commandes shell sans quitter Vim :

| Commande | Action |
|----------|--------|
| `:!ls` | Exécute `ls` et affiche le résultat |
| `:!gcc % -o %<` | Compile le fichier actuel |
| `:r !date` | Insère la sortie de `date` dans le fichier |
| `:.!sort` | Trie la ligne courante |
| `:%!jq .` | Formate tout le fichier avec `jq` (JSON) |

### Folding (pliage de code)

Masquer/afficher des blocs de code.

| Commande | Action |
|----------|--------|
| `zf%` | Créer un fold sur le bloc (curseur sur `{`) |
| `zo` | Ouvrir le fold |
| `zc` | Fermer le fold |
| `za` | Toggle le fold |
| `zR` | Ouvrir tous les folds |
| `zM` | Fermer tous les folds |

**Activer le folding automatique :**
```vim
set foldmethod=syntax   " Selon la syntaxe
set foldmethod=indent   " Selon l'indentation
```

---

## Cheat sheet rapide

### Mouvements essentiels
- `hjkl` → gauche/bas/haut/droite
- `w b e` → mots
- `0 ^ $` → ligne
- `gg G` → fichier

### Édition essentielle
- `i a o` → insertion
- `dd yy p` → supprimer/copier/coller ligne
- `x D C` → supprimer caractère/fin/changer
- `u Ctrl+r .` → undo/redo/répéter

### Text objects essentiels
- `ciw ci" ci( ci{` → changer dans...
- `diw di" di( di{` → supprimer dans...

### Recherche essentielle
- `/mot n N` → chercher/suivant/précédent
- `*` → chercher mot sous curseur
- `:%s/old/new/g` → remplacer

### Fichiers essentiels
- `:w :q :wq` → sauver/quitter
- `Tab Shift+Tab` → naviguer buffers
- `Space + e` → explorateur

### Build essentiels
- `Space + m` → make
- `Space + c` → ouvrir erreurs
- `Space + n/p` → erreur suivante/précédente

---

## Principe fondamental de Vim

> **Verbe + Modificateur + Objet = Action**

| Verbe | Modificateur | Objet | Résultat |
|-------|--------------|-------|----------|
| `d` (delete) | `i` (inner) | `w` (word) | `diw` = supprimer le mot |
| `c` (change) | `i` | `"` (quotes) | `ci"` = changer dans guillemets |
| `y` (yank) | `a` (around) | `{` (braces) | `ya{` = copier avec accolades |
| `v` (visual) | `i` | `t` (tag) | `vit` = sélectionner dans balise |

**C'est comme une langue :** Une fois que tu comprends ce principe, tu peux combiner à l'infini.

---

## Workflow recommandé IDE

### 1. Démarrage projet
```bash
cd mon-projet/
vim src/main.js
```

### 2. Configuration projet
Crée un `.vimrc.local` dans le dossier :
```vim
set makeprg=npm\ test
set tabstop=2 shiftwidth=2
```
Puis charge-le : `:source .vimrc.local`

### 3. Workflow quotidien
1. `Space + e` → ouvre l'explorateur
2. Ouvre des fichiers avec `Enter` (deviennent des buffers)
3. `Tab` / `Shift+Tab` → navigue entre buffers
4. Édite le code
5. `Space + m` → teste/compile
6. `Space + c` → voit les erreurs
7. Corrige et recommence

### 4. Fin de session
```vim
:mksession! .vim.session
:wqa
```

### 5. Reprise
```bash
vim -S .vim.session
```

---

## Ressources complémentaires

### Aide intégrée Vim
```vim
:help keyword       " Aide sur un mot-clé
:help :command      " Aide sur une commande
:help i_CTRL-N      " Aide sur Ctrl+N en mode insertion
:helpgrep pattern   " Chercher dans l'aide
```

### Commandes utiles
```vim
:set filetype?      " Voir le type de fichier détecté
:set                " Voir toutes les options actives
:scriptnames        " Voir les scripts chargés
:version            " Version de Vim
```

---

## À mémoriser en priorité (premiers jours)

### Jour 1 — Survie
- `i` → insérer
- `Esc` → mode normal
- `hjkl` → se déplacer
- `:w` `:q` → sauver/quitter
- `dd` `yy` `p` → supprimer/copier/coller ligne

### Jour 2 — Mouvements
- `w b e` → mots
- `0 $` → ligne
- `gg G` → fichier
- `/mot` `n` → chercher

### Jour 3 — Édition efficace
- `ciw` `ci"` `ci(` → changer dans...
- `u` `Ctrl+r` → undo/redo
- `.` → répéter
- `>` `<` → indenter

### Semaine 1 — Productivité
- `Space + e` → explorateur
- `Tab` → buffers
- `Space + m` → build
- `Ctrl+n` → autocomplétion

---

## Conclusion

Vim a une courbe d'apprentissage, mais une fois maîtrisé :
- Tu édites à la vitesse de ta pensée
- Tes mains ne quittent jamais le clavier
- Tu peux travailler sur n'importe quel serveur (SSH)
- Tu es **beaucoup** plus productif

**Pratique régulière = maîtrise rapide** 🚀

Commence par les commandes essentielles, puis ajoute progressivement les autres.
