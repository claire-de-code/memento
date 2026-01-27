# 🧠 Mémento Vim — Commandes essentielles

## Modes
- `i` : insertion avant le curseur
- `I` : insertion début de ligne
- `a` : insertion après le curseur
- `A` : insertion fin de ligne
- `o` / `O` : nouvelle ligne dessous / dessus
- `Esc` : retour au mode normal
- `v` : sélection visuelle
- `V` : sélection ligne entière
- `Ctrl+v` : sélection en bloc
- `:` : mode commande

---

## Déplacements
- `h j k l` : gauche / bas / haut / droite
- `w` / `b` : mot suivant / précédent
- `e` : fin de mot
- `0` / `^` / `$` : début / premier caractère / fin de ligne
- `gg` / `G` : début / fin du fichier
- `Ctrl+d` / `Ctrl+u` : demi-page bas / haut
- `zz` : centrer la ligne à l’écran

---

## Édition
- `x` : supprimer caractère
- `dd` : supprimer ligne
- `D` : supprimer jusqu’à fin de ligne
- `yy` : copier ligne
- `p` / `P` : coller après / avant
- `u` : annuler
- `Ctrl+r` : rétablir
- `.` : répéter la dernière action

---

## Sélection (mode visuel)
- `v` → sélectionner
- `y` → copier
- `d` → couper
- `>` / `<` → indenter / désindenter
- `=` → auto-indenter

---

## Recherche
- `/mot` : chercher vers le bas
- `?mot` : chercher vers le haut
- `n` / `N` : occurrence suivante / précédente
- `*` : chercher le mot sous le curseur
- `:nohlsearch` : enlever le surlignage

---

## Remplacement
```vim
:%s/ancien/nouveau/g
```
- `%` : tout le fichier
- `g` : toutes les occurrences
- `c` : confirmation

Exemple :
```vim
:%s/foo/bar/gc
```

---

## Fichiers
- `:w` : sauvegarder
- `:q` : quitter
- `:wq` / `:x` : sauvegarder et quitter
- `:q!` : quitter sans sauvegarder
- `:e fichier` : ouvrir un fichier
- `:r fichier` : insérer un fichier

---

## Fenêtres (splits)
- `:split` / `:vsplit` : horizontal / vertical
- `Ctrl+w h j k l` : naviguer entre fenêtres
- `Ctrl+w q` : fermer une fenêtre
- `Ctrl+w =` : équilibrer

---

## Buffers
- `:ls` : liste des buffers
- `:b n` : aller au buffer n
- `:bn` / `:bp` : buffer suivant / précédent
- `:bd` : fermer buffer

---

## Indentation rapide
- `>>` / `<<` : indenter / désindenter une ligne
- `=G` : reformater jusqu’à la fin
- `gg=G` : reformater tout le fichier

---

## Macros
- `qa` : enregistrer macro dans `a`
- `q` : arrêter
- `@a` : rejouer
- `@@` : rejouer la dernière

---

## Commandes shell
```vim
:!commande
```
Exemple :
```vim
:!gcc main.c && ./a.out
```

---

## Astuces indispensables
- `ciw` : changer le mot sous le curseur
- `di(` / `da(` : supprimer dans / avec parenthèses
- `ci"` / `ci'` : changer dans une chaîne
- `gv` : reselectionner la dernière sélection
- `Ctrl+a` / `Ctrl+x` : incrémenter / décrémenter un nombre

---

## Explorateur de fichiers (netrw)

Vim inclut nativement un explorateur de fichiers appelé **netrw** (aucun plugin requis).

### Ouvrir l’explorateur
- `:Ex` / `:Explore` : explorateur dans la fenêtre courante
- `:Vexplore` : explorateur vertical (sidebar)
- `vim .` : ouvrir Vim directement dans un dossier

### Configuration recommandée (sidebar à gauche)
À placer dans le `.vimrc` :

```vim
let g:netrw_banner = 0        " pas de bannière
let g:netrw_liststyle = 3    " vue en arbre
let g:netrw_browse_split = 2 " ouvre les fichiers dans le split opposé
let g:netrw_winsize = 25     " largeur du sidebar
" ne pas définir netrw_altv → split à gauche par défaut
```

Raccourci conseillé :
```vim
nnoremap <leader>e :Vexplore<CR>
```

### Navigation dans netrw
- `Enter` : ouvrir fichier / entrer dans un dossier
- `-` : remonter au dossier parent
- `gh` : afficher / masquer les fichiers cachés
- `%` : créer un nouveau fichier
- `d` : créer un dossier
- `D` : supprimer
- `R` : renommer

---

## Raccourcis de cette configuration (workflow IDE)

Cette section documente **les raccourcis réellement actifs** dans *ton* `.vimrc`.

### Général
- `Space + w` : sauvegarder le fichier
- `Space + q` : quitter la fenêtre
- `Space + x` : sauvegarder et quitter

### Buffers (équivalent des onglets)
- `Tab` : buffer suivant
- `Shift + Tab` : buffer précédent

### Explorateur de fichiers (netrw)
- `Space + e` : ouvrir l’explorateur de fichiers (sidebar à gauche)
- `Enter` (dans netrw) : ouvrir fichier / entrer dans un dossier
- `-` : remonter au dossier parent
- `gh` : afficher / masquer les fichiers cachés

### Recherche
- `/mot` : rechercher dans le fichier
- `n` / `N` : occurrence suivante / précédente
- `Esc Esc` : enlever le surlignage

### Build / Run / Tests (JavaScript / Web)
Ces raccourcis reposent sur `:make`.

Par défaut, Vim utilise la commande définie dans `makeprg`.
Pour un projet JavaScript, on recommande par exemple :

```vim
set makeprg=npm\ run\ build
```

ou :

```vim
set makeprg=npm\ test
```

Raccourcis :
- `Space + m` : sauvegarder + lancer la commande (`make`)
- `Space + c` : ouvrir le panneau d’erreurs (quickfix)
- `Space + n` : erreur suivante
- `Space + p` : erreur précédente

### Autocomplétion native (sans plugin)
- `Ctrl + n` / `Ctrl + p` : compléter par mots du projet
- `Ctrl + x Ctrl + f` : compléter des chemins
- `Ctrl + x Ctrl + l` : compléter des lignes

---

## Vim comme un IDE \(sans plugins\)

### Projet / racine
- `:pwd` : voir le répertoire courant
- Astuce : forcer Vim à se caler sur le dossier courant du projet

```vim
set autochdir
```

### Lancer une commande (build / tests)
- `:!commande` : exécuter une commande shell
- Exemple : `:!make`, `:!pytest`, `:!npm test`

### Quickfix = panneau d’erreurs
- `:make` : lance la commande de build (via `makeprg`)
- `:copen` : ouvrir la liste d’erreurs
- `:cnext` / `:cprev` : erreur suivante / précédente

### Recherche projet
- Recherche dans le fichier : `/mot`, `n`, `N`
- Recherche multi-fichiers (Vim pur) :

```vim
:vimgrep /pattern/ **/*
:copen
```

### Autocomplétion native
- `Ctrl+n` / `Ctrl+p` : compléter par mots du buffer
- `Ctrl+x Ctrl+f` : compléter des chemins
- `Ctrl+x Ctrl+l` : compléter des lignes
- `Ctrl+x Ctrl+o` : omni-completion (si disponible pour le langage)

### Sessions (ouvrir un projet comme un IDE)
- `:mksession! .vim.session` : sauver l’état (buffers/splits)
- `vim -S .vim.session` : recharger l’état

---

## Principe clé
> **Verbe + objet = action**  
> `d` + `w` → `dw`  
> `c` + `i"` → `ci"`

---

## Vim comme IDE (sans plugins)

Vim peut se rapprocher d’un IDE en exploitant uniquement ses fonctionnalités natives.

### Projet et contexte
- `set autochdir` : le répertoire courant suit le fichier actif
- `vim fichier` puis `:Vexplore` : workflow recommandé (éviter `vim .`)

### Compilation & exécution
- `:!commande` : exécuter une commande shell
- `:make` : compiler / lancer les tests (avec quickfix)
- `:copen` : ouvrir le panneau d’erreurs
- `:cnext` / `:cprev` : naviguer dans les erreurs

### Recherche globale
- `/mot` : recherche locale
- `:vimgrep /mot/ **/*` : recherche projet
- `:copen` : parcourir les résultats

### Buffers et navigation
- `:ls` : liste des buffers
- `:bn` / `:bp` : buffer suivant / précédent
- `:bd` : fermer un buffer

### Autocomplétion native
- `Ctrl+n` / `Ctrl+p` : mots du buffer
- `Ctrl+x Ctrl+f` : chemins de fichiers
- `Ctrl+x Ctrl+l` : lignes
- `Ctrl+x Ctrl+o` : omni-completion (selon langage)

### Sessions (ouvrir un projet comme un IDE)
- `:mksession! .vim.session` : sauvegarder l’état
- `vim -S .vim.session` : restaurer la session

---

## À mémoriser en priorité
- `hjkl`, `w b e`
- `dd`, `yy`, `p`
- `ciw`, `ci(`, `ci"`
- `/`, `n`, `N`
- `u`, `Ctrl+r`, `.`
- `:w`, `:q`, `:wq`
- `:Vexplore`, `:make`, `:copen`
- `hjkl`, `w b e`
- `dd`, `yy`, `p`
- `ciw`, `ci(`, `ci"`
- `/`, `n`, `N`
- `u`, `Ctrl+r`, `.`
- `:w`, `:q`, `:wq`

