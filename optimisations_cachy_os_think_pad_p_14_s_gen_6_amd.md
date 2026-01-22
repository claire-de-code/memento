# Optimisations CachyOS — ThinkPad P14s Gen 6 AMD

Ce document est un **mémo pratique** pour optimiser **CachyOS** sur un **ThinkPad P14s Gen 6 AMD** en usage quotidien, avec une base saine pour le jeu (Steam / Proton) **sans sur‑optimisation**.

Objectifs :
- autonomie
- silence
- stabilité
- performances cohérentes

---

## 1. Philosophie générale

- Une **seule** solution de gestion d’énergie
- Pas de tweaks agressifs
- Pas de services concurrents
- Tester une fois, puis oublier

Sur matériel AMD récent, **moins on force, mieux ça marche**.

---

## 2. Gestion CPU & batterie (priorité n°1)

### Installation
```bash
sudo pacman -S auto-cpufreq
```

### Activation
```bash
sudo systemctl enable auto-cpufreq --now
```

### Vérification (ponctuelle)
```bash
sudo auto-cpufreq --monitor
```

À observer :
- fréquences basses en idle
- montées courtes en charge

> Ne pas laisser le monitor ouvert en permanence.

### À ne PAS utiliser en parallèle
```text
- tlp
- power-profiles-daemon
```

---

## 3. Boost CPU (contrôle fin)

Désactiver le boost permanent (hors charge réelle) :
```bash
echo "0" | sudo tee /sys/devices/system/cpu/cpufreq/boost
```

Auto-cpufreq réactivera le boost si nécessaire.

Effets :
- moins de chauffe
- moins de bruit
- meilleure autonomie

---

## 4. GPU AMD (Mesa / RADV)

Installation minimale (souvent déjà présente) :
```bash
sudo pacman -S mesa vulkan-radeon lib32-vulkan-radeon
```

Vérification :
```bash
glxinfo | grep "AMD Radeon"
```

Résultat attendu :
- rendu matériel AMD
- pas de llvmpipe

> Aucun overclock, aucun pilote propriétaire requis.

---

## 5. Luminosité écran (gros gain batterie)

Installation :
```bash
sudo pacman -S brightnessctl
```

Réglage conseillé (intérieur) :
```bash
brightnessctl set 30-40%
```

La luminosité est **le premier facteur de consommation** sur laptop.

---

## 6. Réseau & périphériques

### Wi‑Fi — mode économie
```bash
sudo iw dev wlan0 set power_save on
```

### Bluetooth — désactiver si inutile
```bash
sudo systemctl disable bluetooth --now
```

---

## 7. SSD & maintenance système

### Trim automatique (longévité SSD)
```bash
sudo systemctl enable fstrim.timer --now
```

### Synchronisation horaire
```bash
sudo systemctl enable systemd-timesyncd --now
```

Aucun tweak mount ou NVMe avancé nécessaire.

---

## 8. Steam & Proton (base saine)

### Installation Steam
```bash
sudo pacman -S steam
```

### Proton GE (outil recommandé)
```bash
sudo pacman -S protonup-qt
```

Lancer :
```bash
protonup-qt
```

Utilisation :
- Proton Experimental par défaut
- Proton GE **uniquement par jeu** si problème

---

## 9. GameMode (à activer plus tard)

Optionnel, surtout pour le jeu :
```bash
sudo pacman -S gamemode lib32-gamemode
```

Lancement via Steam :
```text
gamemoderun %command%
```

---

## 10. Ce qu’il ne faut PAS faire

- Forcer le governor performance
- Installer plusieurs gestionnaires d’énergie
- Tweaker sysctl à l’aveugle
- Overclocker l’iGPU
- Bidouiller Vulkan layers

Ces pratiques dégradent souvent autonomie et stabilité.

---

## 11. État final attendu

- machine silencieuse
- températures maîtrisées
- autonomie correcte
- performances stables
- base propre pour Steam / WoW / Proton

---

## 12. Règle d’or

> Sur CachyOS + AMD moderne :
> **observer d’abord, optimiser ensuite, rarement forcer.**

Ce document sert de référence. Une fois appliqué, tu peux l’oublier.

