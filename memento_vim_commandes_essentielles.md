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

## Principe clé
> **Verbe + objet = action**  
> `d` + `w` → `dw`  
> `c` + `i"` → `ci"`

---

## À mémoriser en priorité
- `hjkl`, `w b e`
- `dd`, `yy`, `p`
- `ciw`, `ci(`, `ci"`
- `/`, `n`, `N`
- `u`, `Ctrl+r`, `.`
- `:w`, `:q`, `:wq`

