# 📘 Guide Complet Arch Linux & EndeavourOS

Guide expert pour comprendre, installer et maintenir Arch Linux et EndeavourOS.

---

## 📋 Table des matières

1. [Histoire et philosophie](#histoire-et-philosophie)
2. [Arch vs Debian vs Fedora](#arch-vs-debian-vs-fedora)
3. [EndeavourOS : Arch clé en main](#endeavouros--arch-clé-en-main)
4. [Architecture du système](#architecture-du-système)
5. [Pacman : le gestionnaire de paquets](#pacman--le-gestionnaire-de-paquets)
6. [AUR : Arch User Repository](#aur--arch-user-repository)
7. [Mise à jour sans casser le système](#mise-à-jour-sans-casser-le-système)
8. [Dépannage et récupération](#dépannage-et-récupération)
9. [Optimisation et maintenance](#optimisation-et-maintenance)
10. [Ressources et communauté](#ressources-et-communauté)

---

## Histoire et philosophie

### Naissance d'Arch Linux

**2002** : Judd Vinet crée Arch Linux inspiré par CRUX et BSD.

**Objectif** : Distribution simple, légère, et élégante pour utilisateurs avancés.

**Philosophie K.I.S.S.** (Keep It Simple, Stupid) :
- Simplicité ≠ facilité pour débutants
- Simplicité = transparence du système
- Pas de magie, pas de sur-abstraction
- L'utilisateur garde le contrôle total

**The Arch Way** :
1. **Simplicité** : code propre, configuration claire
2. **Modernité** : dernières versions stables
3. **Pragmatisme** : fonctionnalité avant idéologie
4. **User-centricity** : pour utilisateurs compétents
5. **Versatilité** : système général, pas spécialisé

### Rolling Release

Contrairement aux distributions à versions fixes (Ubuntu 24.04, Fedora 41), Arch adopte le **rolling release** :
- Pas de version majeure
- Mises à jour continues
- Toujours à jour sans réinstallation
- Derniers logiciels disponibles rapidement

**Avantages** :
- Logiciels récents
- Pas de migration majeure
- Corrections de bugs rapides

**Inconvénients** :
- Requiert maintenance régulière
- Risque de casse si négligé
- Nécessite veille technique

### Ligne du temps

```
2002 — Création d'Arch Linux par Judd Vinet
2007 — Aaron Griffin devient lead developer
2012 — systemd adopté comme init system
2013 — Lancement du Arch Wiki (référence mondiale)
2019 — EndeavourOS créé après fin d'Antergos
2024 — Arch reste dans le top 10 DistroWatch
```

---

## Arch vs Debian vs Fedora

### Vue d'ensemble comparative

| Caractéristique | Arch | Debian | Fedora |
|-----------------|------|--------|--------|
| **Philosophie** | KISS, user-centric | Stabilité universelle | Innovation opensource |
| **Modèle release** | Rolling | Stable + Testing + Sid | Semi-rolling (6 mois) |
| **Gestionnaire** | pacman | apt/dpkg | dnf/rpm |
| **Cible** | Avancés | Tous niveaux | Intermédiaires |
| **Fréquence MAJ** | Continue | Stable: 2 ans | 6 mois |
| **Support LTS** | N/A | 5 ans | 13 mois |
| **Init system** | systemd | systemd (sysvinit option) | systemd |
| **Packages** | ~13k officiels + AUR | ~59k | ~80k |
| **Entreprise** | Communauté | Communauté | Red Hat/IBM |

### Installation de base

**Arch** :
```bash
# Installation manuelle complète
fdisk → mkfs → mount → pacstrap → genfstab → arch-chroot
# 100% contrôle, 100% responsabilité
```

**Debian** :
```bash
# Installateur graphique guidé
# Choix desktop, tâches prédéfinies
# Prêt à l'emploi
```

**Fedora** :
```bash
# Anaconda installer (graphique)
# Workstation/Server/IoT editions
# Dernières techno (Wayland, PipeWire)
```

### Gestion des paquets en détail

#### Arch (pacman)

**Syntaxe claire** :
```bash
pacman -S package    # Sync (install)
pacman -R package    # Remove
pacman -Ss keyword   # Search
pacman -Q            # Query installed
```

**Base de données locale** :
- `/var/lib/pacman/` contient l'état du système
- Fichiers `.PKGINFO` pour chaque paquet
- Très rapide, pas de résolution complexe

**Dépendances** :
- Résolution stricte et directe
- Pas de "recommended packages"
- Dépendances optionnelles explicites

#### Debian (apt)

```bash
apt install package
apt remove package
apt search keyword
dpkg -l             # Liste paquets
```

**Complexité** :
- Gestion sophisticated des dépendances
- Priorités, suggestions, recommandations
- Politique de stabilité stricte

**Versions multiples** :
- Stable : vieux mais sûr
- Testing : équilibre
- Sid : bleeding edge

#### Fedora (dnf)

```bash
dnf install package
dnf remove package
dnf search keyword
rpm -qa             # Liste RPM
```

**Caractéristiques** :
- Successeur de yum (plus rapide)
- Modules et streams (versions multiples)
- Focus innovation (SELinux par défaut)

### Philosophie de stabilité

**Arch** :
- Stabilité = logiciels testés récents
- "Stable" ≠ "ancien"
- Confiance dans upstream
- Utilisateur responsable de tester

**Debian** :
- Stabilité = immobilisme calculé
- Freeze avant release
- Backports pour versions récentes
- "When it's ready"

**Fedora** :
- Stabilité = cutting edge maîtrisé
- Beta testing avant release
- Technologie Red Hat Enterprise Linux
- Équilibre innovation/fiabilité

### Cas d'usage typiques

**Arch** :
- Développeurs voulant contrôle total
- Stations de travail personnalisées
- Apprentissage Linux approfondi
- Serveurs personnels (avec précaution)

**Debian** :
- Serveurs production critiques
- Infrastructure stable long terme
- Systèmes embarqués
- Usage général conservateur

**Fedora** :
- Développeurs Red Hat ecosystem
- Stations de travail modernes
- Testing nouvelles technos
- Serveurs avec lifecycle court

---

## EndeavourOS : Arch clé en main

### Historique

**2019** : Création après la fin d'Antergos (autre Arch dérivée).

**Équipe** : Communauté de passionnés, pas d'entreprise.

**Mission** : "Arch sans la peine de l'installation".

### Philosophie

EndeavourOS n'est **PAS** :
- Une distribution séparée
- Une surcouche lourde
- Un fork d'Arch

EndeavourOS **EST** :
- Arch Linux pur avec installateur
- Configurations communautaires sensées
- Support communautaire accessible
- Pont vers Arch pour débutants

### Différences techniques avec Arch vanilla

| Aspect | Arch vanilla | EndeavourOS |
|--------|-------------|-------------|
| **Installation** | archinstall ou manuelle | Calamares (GUI) |
| **Dépôts** | core, extra, multilib | + endeavouros repo |
| **Packages de base** | Minimal | + yay, reflector, etc. |
| **Desktop** | Aucun | Choix lors install |
| **Configuration** | Manuelle | Préconfigurée |
| **Thème** | Vanilla | Thème spatial violet |
| **Wallpapers** | Aucun | Collection EndeavourOS |
| **Welcome app** | Non | Oui (eos-welcome) |

### Paquet `eos-*`

EndeavourOS ajoute des outils dans son dépôt :

```bash
# Outils EndeavourOS
eos-update-notifier    # Notifications MAJ
eos-log-tool           # Logs système
eos-rankmirrors        # Optimiser miroirs
eos-bash-shared        # Fonctions bash
eos-hooks              # Hooks pacman
```

**Important** : Ces paquets ne modifient **PAS** le système Arch sous-jacent.

### Avantages EndeavourOS

**Pour nouveaux à Arch** :
- Installation en 15 minutes vs 2 heures
- Configuration DE prête
- Drivers graphiques auto-détectés
- Communauté accueillante

**Pour utilisateurs expérimentés** :
- Gain de temps sur installation répétitive
- Base solide pour personnalisation
- Même flexibilité qu'Arch
- Arch Wiki toujours applicable

### Transition EndeavourOS → Arch pur

Possible et facile :
```bash
# Supprimer dépôt EndeavourOS
sudo sed -i '/endeavouros/d' /etc/pacman.conf

# Supprimer paquets eos-*
sudo pacman -Rns $(pacman -Qq | grep eos-)

# Continuer comme Arch vanilla
```

Résultat : système Arch pur, sans trace EndeavourOS.

---

## Architecture du système

### Hiérarchie des dépôts Arch

```
[core]          — Paquets essentiels (kernel, systemd, base)
    ↓
[extra]         — Paquets officiels additionnels (DE, apps)
    ↓
[multilib]      — Support 32-bit sur systèmes 64-bit
    ↓
[testing]       — Paquets en test (opt-in)
    ↓
AUR             — Scripts communautaires (non-officiel)
```

**core** :
- ~250 paquets
- Système bootable minimal
- Maintenance TU (Trusted Users)

**extra** :
- ~13,000 paquets
- Environnements desktop
- Applications courantes

**multilib** :
- Bibliothèques 32-bit
- Wine, Steam, etc.

**testing** :
- Nouveaux paquets majeurs
- 1-2 semaines avant stable
- Activation manuelle requise

### Structure pacman

```
/etc/pacman.conf           — Configuration principale
/etc/pacman.d/mirrorlist   — Liste des miroirs
/var/lib/pacman/           — Base de données paquets
/var/cache/pacman/pkg/     — Cache paquets téléchargés
```

**pacman.conf** sections importantes :
```ini
[options]
Architecture = auto
CheckSpace               # Vérifie espace disque
Color                    # Sortie colorée
ParallelDownloads = 5    # Téléchargements parallèles

[core]
Include = /etc/pacman.d/mirrorlist

[extra]
Include = /etc/pacman.d/mirrorlist

[multilib]
Include = /etc/pacman.d/mirrorlist
```

### Miroirs et reflector

**Miroirs** = serveurs hébergeant les paquets Arch.

**Problème** : tous les miroirs ne sont pas égaux (vitesse, fraîcheur).

**Solution** : `reflector` (installé par défaut sur EndeavourOS).

```bash
# Mettre à jour mirrorlist automatiquement
sudo reflector --country France,Germany \
               --age 12 \
               --protocol https \
               --sort rate \
               --save /etc/pacman.d/mirrorlist

# Automatiser avec systemd timer
sudo systemctl enable reflector.timer
```

**EndeavourOS** active reflector par défaut.

### Base system vs base-devel

**base** :
- Système minimal bootable
- ~100 paquets
- Shell, coreutils, kernel

**base-devel** :
- Outils de compilation
- gcc, make, autoconf
- **Requis pour AUR**

```bash
# Installer base-devel (si manquant)
sudo pacman -S --needed base-devel
```

---

## Pacman : le gestionnaire de paquets

### Commandes essentielles

```bash
# SYNCHRONISER (installer)
sudo pacman -S package              # Installer
sudo pacman -S package1 package2    # Multiple
sudo pacman -Sy                     # Sync database
sudo pacman -Syu                    # Sync + upgrade
sudo pacman -Syyu                   # Force sync + upgrade

# RECHERCHER
pacman -Ss keyword                  # Search remote
pacman -Si package                  # Info remote

# REQUÊTES LOCALES
pacman -Q                           # Tous paquets installés
pacman -Qq                          # Liste simple
pacman -Qe                          # Explicitement installés
pacman -Qd                          # Dépendances
pacman -Qdt                         # Dépendances orphelines
pacman -Ql package                  # Fichiers du paquet
pacman -Qo /path/to/file            # Paquet propriétaire

# SUPPRIMER
sudo pacman -R package              # Remove
sudo pacman -Rs package             # + dépendances
sudo pacman -Rns package            # + config + dépendances
sudo pacman -Rdd package            # Force (dangereux)

# CACHE
sudo pacman -Sc                     # Nettoyer cache
sudo pacman -Scc                    # Tout nettoyer
```

### Flags importants

| Flag | Signification |
|------|---------------|
| `-S` | Sync (install from repos) |
| `-R` | Remove |
| `-Q` | Query (local database) |
| `-y` | Refresh database |
| `-u` | Upgrade |
| `-s` | Search |
| `-i` | Info |
| `-c` | Clean cache |
| `-n` | No backup (.pacsave) |
| `-d` | Dependencies |
| `-t` | Orphans |

### Hooks pacman

Les hooks s'exécutent avant/après opérations pacman.

**Localisation** : `/usr/share/libalpm/hooks/` et `/etc/pacman.d/hooks/`

**Exemple EndeavourOS** : `eos-reboot-required.hook`
```ini
[Trigger]
Type = Package
Operation = Upgrade
Target = linux
Target = systemd

[Action]
Description = Checking if reboot is required...
When = PostTransaction
Exec = /usr/bin/eos-reboot-required
```

Affiche notification si redémarrage nécessaire après MAJ kernel.

### Fichiers .pacnew et .pacsave

**Situation** : Tu modifies `/etc/pacman.conf`, puis pacman veut le mettre à jour.

**Comportement** :
- Ton fichier : `/etc/pacman.conf` (préservé)
- Nouveau : `/etc/pacman.conf.pacnew` (créé)

**Action requise** : Merger manuellement les changements.

**Outil** : `pacdiff` (dans `pacman-contrib`)

```bash
# Installer pacdiff
sudo pacman -S pacman-contrib

# Gérer fichiers .pacnew/.pacsave
sudo DIFFPROG=vim pacdiff

# Ou utiliser un outil graphique
yay -S meld
sudo DIFFPROG=meld pacdiff
```

**Workflow** :
1. Après `pacman -Syu`, vérifier messages
2. Si `.pacnew` mentionné, lancer `pacdiff`
3. Comparer et merger
4. Supprimer `.pacnew` une fois traité

**Fichiers critiques à surveiller** :
- `/etc/pacman.conf`
- `/etc/pacman.d/mirrorlist`
- `/etc/fstab`
- `/etc/mkinitcpio.conf`
- `/boot/loader/entries/*.conf` (systemd-boot)

---

## AUR : Arch User Repository

### Qu'est-ce que l'AUR ?

**AUR** ≠ dépôt binaire officiel.

**AUR** = collection de **PKGBUILD** (scripts de build).

**Contenu** :
- ~90,000+ paquets communautaires
- Logiciels propriétaires (Google Chrome, Spotify)
- Logiciels niche non dans repos officiels
- Versions git/beta/rc

**Hébergement** : https://aur.archlinux.org/

### Architecture AUR

```
Utilisateur crée PKGBUILD
    ↓
Upload sur AUR (git push)
    ↓
Communauté vote et commente
    ↓
TU peut adopter → repos officiels
    ↓
Ou reste dans AUR
```

**PKGBUILD** = recette bash :
```bash
# Exemple simplifié
pkgname=myapp
pkgver=1.0.0
source=("https://github.com/user/myapp/archive/$pkgver.tar.gz")

build() {
    cd "$pkgname-$pkgver"
    make
}

package() {
    cd "$pkgname-$pkgver"
    make DESTDIR="$pkgdir" install
}
```

### Sécurité AUR

**IMPORTANT** : L'AUR n'est **PAS** vérifié par Arch.

**Risques** :
- Code malveillant dans PKGBUILD
- Source compromise
- Maintainer malintentionné

**Protection** :
1. **Lire le PKGBUILD** avant installation
2. Vérifier popularité et votes
3. Checker dernière mise à jour
4. Regarder commentaires

**Exemple vérification** :
```bash
# Télécharger et inspecter
git clone https://aur.archlinux.org/package-name.git
cd package-name
cat PKGBUILD    # LIRE ATTENTIVEMENT

# Vérifier source
cat .SRCINFO

# Si OK, build
makepkg -si
```

**Red flags** :
- Commandes `curl | bash`
- `chmod 777` suspects
- Téléchargements depuis domaines douteux
- Peu de votes avec package ancien
- Maintainer inconnu avec paquet récent

### Helpers AUR

**Helpers** automatisent le workflow AUR.

**Populaires** :
- `yay` (Yet Another Yogurt) — écrit en Go
- `paru` — écrit en Rust, plus strict
- `pikaur` — écrit en Python

**EndeavourOS** installe `yay` par défaut.

#### yay

```bash
# Installer paquet AUR
yay -S package-name

# Rechercher dans AUR
yay -Ss keyword

# Mettre à jour AUR + officiels
yay -Syu

# Mettre à jour uniquement AUR
yay -Sua

# Infos paquet AUR
yay -Si package-name

# Build sans installer
yay -G package-name
cd package-name
makepkg -si
```

**Options utiles** :
```bash
yay -Syu --devel       # MAJ aussi packages *-git
yay -Syu --timeupdate  # Trier par date
yay -Ps                # Stats système
yay -Yc                # Nettoyer cache AUR
```

#### paru (alternative stricte)

```bash
sudo pacman -S paru

# Syntaxe identique à yay
paru -Syu

# Mais comportement plus strict
# Affiche PKGBUILD automatiquement
# Review code obligatoire
```

### Maintenir packages AUR

**Adopted packages** : mainteneur actif.

**Orphaned packages** : aucun mainteneur.

**Out-of-date** : version obsolète signalée.

**Tu peux** :
- Signaler out-of-date
- Commenter pour bugs
- Proposer patches
- Adopter paquet orphelin (si TU ou contributeur)

---

## Mise à jour sans casser le système

### Philosophie rolling release

**Arch n'est pas Ubuntu** :
- Pas de version fixe
- Changements continus
- Responsabilité utilisateur

**Règle d'or** : 
> Ne jamais faire `pacman -Syu` puis partir en vacances.

### Fréquence de mise à jour

**Recommandé** : 1 fois par semaine minimum.

**Pourquoi** :
- Évite accumuler changements cassants
- Plus facile de diagnostiquer problèmes récents
- Sécurité (CVE patches rapides)

**Trop long sans MAJ** (>1 mois) :
- Risque de conflit dépendances
- Partial upgrades risqués
- Possible cassure système

### Workflow de mise à jour sécurisé

#### Étape 1 : Vérifier les actualités

**TOUJOURS** consulter https://archlinux.org/news/ avant MAJ.

**Actualités critiques** :
- Changements manuels requis
- Migrations de paquets
- Incompatibilités connues

**Exemple historique** :
```
2024-01-15: Python 3.12 migration
Action requise: Rebuild AUR packages Python

2023-06-01: /usr merge
Action requise: Vérifier /bin → /usr/bin
```

#### Étape 2 : Backup (si critique)

```bash
# Snapshot Btrfs (si configuré)
sudo btrfs subvolume snapshot / /.snapshots/before-update-$(date +%F)

# Ou backup traditionnel
sudo rsync -aAXv / /mnt/backup/ --exclude={"/dev/*","/proc/*","/sys/*"}

# Timeshift (outil graphique)
yay -S timeshift
```

#### Étape 3 : Mettre à jour mirrorlist

```bash
# EndeavourOS : reflector intégré
sudo reflector --country France,Germany,Netherlands \
               --age 12 \
               --protocol https \
               --sort rate \
               --save /etc/pacman.d/mirrorlist

# Ou manuellement
sudo pacman-mirrors --country France --geoip
```

#### Étape 4 : Mise à jour

```bash
# Sync database
sudo pacman -Sy

# Voir ce qui va être mis à jour
sudo pacman -Qu

# Mettre à jour
sudo pacman -Syu

# Surveiller sortie pour :
# - Conflits
# - Fichiers .pacnew
# - Warnings
```

#### Étape 5 : Traiter .pacnew

```bash
sudo pacdiff

# Ou manuellement
find /etc -name "*.pacnew"
```

#### Étape 6 : Mettre à jour AUR

```bash
yay -Sua

# Lire PKGBUILD modifiés
# Confirmer builds
```

#### Étape 7 : Vérifier système

```bash
# Services en erreur
systemctl --failed

# Logs récents
journalctl -p 3 -xb

# Kernel actuel vs installé
uname -r
pacman -Q linux
```

#### Étape 8 : Redémarrer si nécessaire

**Quand redémarrer** :
- Kernel mis à jour
- systemd mis à jour
- glibc mis à jour
- Mesa/drivers graphiques (optionnel)

```bash
# EndeavourOS affiche notification auto
# Ou vérifier
cat /var/lib/eos-reboot-required 2>/dev/null
```

### Éviter partial upgrades

**Partial upgrade** = installer paquet sans mettre à jour dépendances.

**JAMAIS faire** :
```bash
sudo pacman -S package    # Sans -Syu avant
```

**Pourquoi** :
- Paquet attend version dépendance récente
- Système actuel a version ancienne
- Cassure garantie

**TOUJOURS faire** :
```bash
sudo pacman -Syu          # D'abord
sudo pacman -S package    # Puis installer
```

### Gérer conflits de paquets

**Scénario** : `pacman -Syu` dit "conflict detected".

**Exemple** :
```
conflict between package-a and package-b
package-b: /usr/bin/tool exists in filesystem
```

**Solution** :
```bash
# Supprimer paquet conflictuel
sudo pacman -Rdd package-b

# Réessayer MAJ
sudo pacman -Syu
```

**Si fichier orphelin** :
```bash
# Forcer overwrite (ATTENTION)
sudo pacman -Syu --overwrite /usr/bin/tool
```

### Problèmes signatures PGP

**Erreur** : "signature from X is unknown trust".

**Causes** :
- Clé expirée
- Keyring non à jour
- MAJ longtemps négligée

**Solutions** :

```bash
# 1. Mettre à jour keyring
sudo pacman -Sy archlinux-keyring

# 2. Puis MAJ normale
sudo pacman -Su

# 3. Si persistant, rafraîchir clés
sudo pacman-key --refresh-keys

# 4. Dernier recours, réinit keyring
sudo rm -rf /etc/pacman.d/gnupg
sudo pacman-key --init
sudo pacman-key --populate archlinux
```

**EndeavourOS** :
```bash
sudo pacman -Sy archlinux-keyring endeavouros-keyring
```

### Downgrade en cas de régression

**Scénario** : Paquet mis à jour cause bug.

**Solution 1 : Cache pacman**

```bash
# Lister versions en cache
ls /var/cache/pacman/pkg/ | grep package-name

# Downgrade
sudo pacman -U /var/cache/pacman/pkg/package-name-1.0-1-x86_64.pkg.tar.zst
```

**Solution 2 : Arch Linux Archive**

```bash
# Ajouter miroir archive
# /etc/pacman.conf
[core]
Server = https://archive.archlinux.org/repos/2024/01/15/$repo/os/$arch

# Downgrade
sudo pacman -Syu package-name
```

**Solution 3 : downgrade tool**

```bash
yay -S downgrade

# Utiliser
sudo downgrade package-name
# Interface interactive avec versions disponibles
```

**Bloquer MAJ temporairement** :
```bash
# /etc/pacman.conf
IgnorePkg = package-name

# Ou
sudo pacman -S package-name --ignore package-name
```

---

## Dépannage et récupération

### Système ne boote plus

#### chroot depuis live USB

```bash
# Booter EndeavourOS live USB

# Monter partitions
sudo mount /dev/sdXY /mnt              # root
sudo mount /dev/sdXZ /mnt/boot         # boot (si séparée)
sudo mount /dev/sdXW /mnt/boot/efi     # EFI (si UEFI)

# Monter systèmes virtuels
sudo mount -t proc /proc /mnt/proc
sudo mount -t sysfs /sys /mnt/sys
sudo mount --rbind /dev /mnt/dev
sudo mount --rbind /run /mnt/run

# Chroot
sudo chroot /mnt /bin/bash

# Maintenant tu es dans ton système cassé
# Réparer...
```

#### Réparer bootloader

**systemd-boot** :
```bash
bootctl install
```

**GRUB** :
```bash
grub-install --target=x86_64-efi --efi-directory=/boot/efi
grub-mkconfig -o /boot/grub/grub.cfg
```

#### Réparer kernel

```bash
# Réinstaller kernel
pacman -S linux

# Régénérer initramfs
mkinitcpio -P

# Si erreurs, vérifier
pacman -S base linux linux-firmware
```

### Dépendances cassées

**Erreur** : "failed to prepare transaction (could not satisfy dependencies)".

**Solution** :
```bash
# Forcer réinstallation base
sudo pacman -S base --overwrite "*"

# Reconstruire database
sudo pacman -Qkk

# Dernier recours
sudo pacman -Syyu --overwrite "*"
```

### Espace disque plein

```bash
# Nettoyer cache pacman
sudo pacman -Scc

# Supprimer orphelins
sudo pacman -Rns $(pacman -Qtdq)

# Nettoyer journalctl
sudo journalctl --vacuum-size=100M

# Trouver gros fichiers
sudo du -h / | grep '^[0-9\.]\+G'
```

### Fichiers corrompus

```bash
# Vérifier intégrité paquets
sudo pacman -Qkk

# Réinstaller paquet corrompu
sudo pacman -S package-name --overwrite "*"
```

---

## Optimisation et maintenance

### Nettoyer le système

```bash
# Orphelins
sudo pacman -Rns $(pacman -Qtdq)

# Cache pacman (garder 3 dernières versions)
sudo paccache -rk3

# Ou tout supprimer
sudo pacman -Scc

# Cache AUR (yay)
yay -Sc

# Journaux
sudo journalctl --vacuum-time=2weeks

# Tmp
sudo rm -rf /tmp/*
```

### Optimiser pacman

**Parallel downloads** :
```bash
# /etc/pacman.conf
ParallelDownloads = 5
```

**Meilleurs miroirs** :
```bash
sudo reflector --latest 20 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```

**Activer couleurs** :
```bash
# /etc/pacman.conf
Color
```

### Surveiller performances

```bash
# Temps de boot
systemd-analyze

# Services lents
systemd-analyze blame

# Chaîne critique
systemd-analyze critical-chain

# Utilisation RAM
ps_mem

# I/O disque
iotop
```

### Automatiser maintenance

**Script hebdomadaire** :
```bash
#!/bin/bash
# ~/bin/arch-maintenance.sh

echo "=== Arch Maintenance ==="

# MAJ système
echo "Updating system..."
yay -Syu --noconfirm

# Nettoyer orphelins
echo "Removing orphans..."
sudo pacman -Rns $(pacman -Qtdq) --noconfirm 2>/dev/null

# Cache
echo "Cleaning cache..."
yay -Sc --noconfirm
sudo paccache -rk3

# Logs
echo "Cleaning journals..."
sudo journalctl --vacuum-time=2weeks

echo "Done!"
```

**Systemd timer** :
```ini
# /etc/systemd/system/maintenance.timer
[Unit]
Description=Weekly maintenance

[Timer]
OnCalendar=weekly
Persistent=true

[Install]
WantedBy=timers.target
```

```ini
# /etc/systemd/system/maintenance.service
[Unit]
Description=System maintenance

[Service]
Type=oneshot
ExecStart=/home/user/bin/arch-maintenance.sh
```

Activer :
```bash
sudo systemctl enable --now maintenance.timer
```

---

## Ressources et communauté

### Documentation officielle

**Arch Wiki** : https://wiki.archlinux.org/
- Référence absolue Linux
- Qualité exceptionnelle
- Applicable à toutes distributions
- Traduit en français partiel

**Sections essentielles** :
- Installation guide
- General recommendations
- Pacman
- AUR
- systemd
- Networking

### EndeavourOS

**Site** : https://endeavouros.com/

**Forum** : https://forum.endeavouros.com/
- Très actif
- Communauté bienveillante
- Support rapide

**Wiki** : https://discovery.endeavouros.com/

### Actualités

**Arch Linux** :
- https://archlinux.org/news/
- **À consulter avant CHAQUE mise à jour**

**Planet Arch** : https://planet.archlinux.org/
- Blogs développeurs et TU

### Communauté française

**Forum Arch Linux FR** : https://forums.archlinux.fr/

**IRC/Discord** :
- #archlinux-fr sur Libera.Chat
- Discord EndeavourOS (international)

### Contribuer

**Arch** :
- Soumettre PKGBUILD à AUR
- Améliorer Wiki
- Reporter bugs
- Devenir TU (processus long)

**EndeavourOS** :
- Forum support
- Tester ISO
- Proposer thèmes
- Documentation

### Commandes de secours

**Carte de référence rapide** :

```bash
# MAJ sécurisée
sudo pacman -Syu

# Rechercher
pacman -Ss package

# Infos
pacman -Si package
pacman -Qi package

# Fichiers d'un paquet
pacman -Ql package

# Propriétaire fichier
pacman -Qo /path/to/file

# Orphelins
pacman -Qtd

# Nettoyer
sudo pacman -Rns $(pacman -Qtdq)
sudo paccache -rk3

# AUR
yay -S package
yay -Sua

# Downgrade
sudo pacman -U /var/cache/pacman/pkg/package.pkg.tar.zst

# Fichiers .pacnew
sudo pacdiff

# Chroot rescue
sudo mount /dev/sdXY /mnt
sudo arch-chroot /mnt
```

---

## Checklist maintenance mensuelle

```
[ ] Consulter archlinux.org/news
[ ] sudo pacman -Syu
[ ] yay -Sua
[ ] sudo pacdiff
[ ] sudo pacman -Rns $(pacman -Qtdq)
[ ] sudo paccache -rk3
[ ] sudo journalctl --vacuum-time=1month
[ ] systemctl --failed (vérifier)
[ ] Backup important
```

---

## Conclusion

**Arch/EndeavourOS** est stable et fiable **SI** :
- Mises à jour régulières (hebdomadaires)
- Lecture des news avant MAJ
- Compréhension du système
- Responsabilité utilisateur

**Avantages** :
- Toujours à jour
- Performances excellentes
- Contrôle total
- Apprentissage Linux

**Ce n'est PAS** :
- Une distribution "install and forget"
- Pour débutants complets Linux
- Pour serveurs critiques sans surveillance

**EndeavourOS** rend Arch accessible sans sacrifier la philosophie.

**The Arch Way** : Simple, élégant, et entre tes mains.
