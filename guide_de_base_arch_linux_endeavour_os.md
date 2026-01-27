# Arch Linux / EndeavourOS — Guide de base des commandes

Ce guide est volontairement **court, pratique et orienté usage quotidien**. Il couvre l’essentiel pour **installer des logiciels**, **mettre à jour le système**, et comprendre **AUR, AppImage et Flatpak** sans se perdre.

---

## 1. Gestion des paquets officiels — pacman

Arch utilise **pacman**, un gestionnaire simple, rapide et très lisible.

### Mettre à jour le système (commande la plus importante)

```bash
sudo pacman -Syu
```

- `-S` : synchroniser / installer
- `-y` : rafraîchir la base de paquets
- `-u` : mettre à jour tous les paquets installés

👉 À faire **régulièrement**, mais pas à l’aveugle avant une session critique.

---

### Installer un paquet

```bash
sudo pacman -S firefox
```

---

### Supprimer un paquet

```bash
sudo pacman -R firefox
```

Supprimer **avec dépendances inutiles** :

```bash
sudo pacman -Rns firefox
```

---

### Rechercher un paquet

```bash
pacman -Ss nom_du_paquet
```

---

### Nettoyer le cache (occasionnel)

```bash
sudo pacman -Sc
```

---

## 2. L’AUR — Arch User Repository

L’**AUR** n’est pas un dépôt officiel.
C’est une collection de **PKGBUILD** (recettes de compilation).

👉 Quand tu installes depuis l’AUR, **tu fais confiance au script**.

Règle simple :
> AUR = utile, mais pas automatique.

---

## 3. yay — gestionnaire AUR (recommandé)

EndeavourOS installe généralement **yay** par défaut.

### Mettre à jour tout (officiel + AUR)

```bash
yay
```

ou explicitement :

```bash
yay -Syu
```

---

### Installer un paquet AUR

```bash
yay -S nom_du_paquet
```

Exemple :

```bash
yay -S google-chrome
```

---

### Ce que fait yay (important)

- télécharge le PKGBUILD
- te montre le contenu
- compile localement
- installe le paquet

👉 Lis **au moins une fois** le PKGBUILD si le paquet est sensible.

---

## 4. AppImage — applications autonomes

**AppImage** = un fichier, une appli.
Pas d’installation système.

### Utilisation

```bash
chmod +x MonAppli.AppImage
./MonAppli.AppImage
```

Avantages :
- zéro dépendance
- facile à tester

Inconvénients :
- pas de mises à jour automatiques
- pas intégré au système

👉 Idéal pour tester ou pour des outils ponctuels.

---

## 5. Flatpak — applications sandboxées

Flatpak est **indépendant de pacman**.
Il fonctionne avec des runtimes.

### Installer Flatpak

```bash
sudo pacman -S flatpak
```

Ajouter Flathub :

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

---

### Installer une application Flatpak

```bash
flatpak install flathub org.mozilla.firefox
```

---

### Lancer une application Flatpak

```bash
flatpak run org.mozilla.firefox
```

---

### Mettre à jour les Flatpak

```bash
flatpak update
```

---

## 6. Quelle méthode choisir ?

| Besoin | Solution recommandée |
|------|----------------------|
| Paquets système | pacman |
| Logiciels absents des dépôts | yay (AUR) |
| Test rapide / portable | AppImage |
| Appli graphique isolée | Flatpak |

---

## 7. Règle d’or Arch / EndeavourOS

- pacman pour le système
- AUR avec parcimonie
- Flatpak pour les grosses apps graphiques
- AppImage pour tester

Si tu respectes ça, Arch reste **stable, lisible et agréable**.

---

## Commande à retenir par cœur

```bash
sudo pacman -Syu
```

Tout commence (et se termine) par là.

