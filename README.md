# Koredge Standup

L'app de bureau de Koredge pour suivre et piloter ses sessions Claude Code : l'appel de l'équipe, le chat avec chaque session, les permissions, la file de prompts et les notifications.

Version actuelle : **1.1.0** · [Toutes les versions et leurs nouveautés](https://github.com/DylanSS98/kstandup-releases/releases)

## Avant d'installer

L'app lit les sessions de Claude Code **de la machine où elle tourne**. Il faut donc que Claude Code soit installé et connecté à cet endroit : la commande `claude` doit répondre dans un terminal.

**Sous Windows, choisis selon l'endroit où tu utilises Claude Code :**
- dans PowerShell ou le Terminal Windows → la **version Windows** ;
- dans WSL (Ubuntu…) → la **version Linux**, installée dans WSL.

## Quel fichier télécharger

| Système | Fichier |
|---|---|
| Mac Apple Silicon (M1, M2, M3, M4…) | [Koredge-Standup-1.1.0-arm64.zip](https://github.com/DylanSS98/kstandup-releases/releases/latest/download/Koredge-Standup-1.1.0-arm64.zip) |
| Mac Intel | [Koredge-Standup-1.1.0-x64.zip](https://github.com/DylanSS98/kstandup-releases/releases/latest/download/Koredge-Standup-1.1.0-x64.zip) |
| Windows 10 et 11 (64 bits) | [Koredge-Standup-1.1.0-win32-x64.zip](https://github.com/DylanSS98/kstandup-releases/releases/latest/download/Koredge-Standup-1.1.0-win32-x64.zip) |
| Linux et WSL (64 bits) | [Koredge-Standup-1.1.0-linux-x64.tar.gz](https://github.com/DylanSS98/kstandup-releases/releases/latest/download/Koredge-Standup-1.1.0-linux-x64.tar.gz) |

Sur Mac, pour savoir lequel prendre : menu  › À propos de ce Mac, ligne « Puce » (Apple) ou « Processeur » (Intel).

## Mac

1. Ouvre le zip : il donne **Koredge Standup.app**. Glisse-la dans **Applications**.
2. Premier lancement : **clic droit sur l'app › Ouvrir**, puis Ouvrir. L'app n'est pas signée par Apple, macOS demande donc une confirmation une fois. Si le bouton n'apparaît pas : Réglages Système › Confidentialité et sécurité › **Ouvrir quand même**.

## Windows

1. Télécharge le zip. Avant de l'ouvrir : **clic droit › Propriétés**, coche **Débloquer** en bas, puis OK. Windows ne bloquera alors pas chaque fichier extrait.
2. **Clic droit › Extraire tout…** vers un dossier à toi, par exemple `%LOCALAPPDATA%\Programs`. Évite `C:\Program Files` : l'app ne pourrait pas s'y mettre à jour toute seule.
3. Dans le dossier `Koredge Standup-win32-x64`, lance **koredge-standup.exe**.
4. Si Windows affiche « Windows a protégé votre ordinateur » : **Informations complémentaires › Exécuter quand même**. L'app n'est pas signée par un certificat payant, d'où l'avertissement.

Au premier lancement, l'app s'ajoute au **menu Démarrer**. Son icône reste dans la zone de notification, en bas à droite : fermer la fenêtre ne quitte pas l'app. Pour la quitter : clic droit sur l'icône › Quit.

## Linux et WSL

### Dans WSL

Il faut **WSL 2 avec WSLg**, qui affiche les fenêtres des apps Linux sur le bureau Windows. Il est inclus dans Windows 11 et dans Windows 10 à jour (WSL installé depuis le Microsoft Store). Pour vérifier ou mettre à jour, dans PowerShell :

```powershell
wsl --update
wsl --version
```

Puis, **dans le terminal WSL** (Ubuntu) :

```bash
# les bibliothèques dont l'app a besoin (une seule fois)
sudo apt update
sudo apt install -y libgtk-3-0 libnss3 libgbm1 libxss1 libxtst6 libnotify4
sudo apt install -y libasound2t64 || sudo apt install -y libasound2

# l'app, dans ton dossier personnel
cd ~
curl -LO https://github.com/DylanSS98/kstandup-releases/releases/latest/download/Koredge-Standup-1.1.0-linux-x64.tar.gz
tar -xzf Koredge-Standup-1.1.0-linux-x64.tar.gz && rm Koredge-Standup-1.1.0-linux-x64.tar.gz
"./Koredge Standup-linux-x64/koredge-standup"
```

La fenêtre s'ouvre sur le bureau Windows. Après ce premier lancement, l'app apparaît aussi dans le **menu Démarrer de Windows**, dans le dossier de ta distribution (par exemple « Ubuntu »).

Sous WSL, l'icône dans la zone de notification et les notifications dépendent de WSLg et peuvent ne pas s'afficher. Fermer la fenêtre quitte l'app.

### Linux

Les mêmes commandes que pour WSL, à partir de la deuxième étape. Sur une autre distribution qu'Ubuntu ou Debian, installe l'équivalent de ces bibliothèques avec son gestionnaire de paquets.

### Si l'app ne démarre pas

- Message « The SUID sandbox helper binary was found, but is not configured correctly » : lance-la avec `--no-sandbox` :
  ```bash
  "./Koredge Standup-linux-x64/koredge-standup" --no-sandbox
  ```
  L'app le garde ensuite pour ses mises à jour et pour son entrée dans le menu. C'est un dernier recours : cette option coupe une protection de Chromium. Ce message apparaît surtout sur Ubuntu 24.04 installé directement sur un PC, rarement sous WSL.
- Message « error while loading shared libraries: libXXX.so » : la bibliothèque manque. Cherche le paquet qui la fournit, par exemple avec `apt-file search libXXX.so`, et installe-le.

## Mises à jour

L'app cherche une nouvelle version au démarrage puis toutes les 6 heures, et te prévient par une notification. On peut aussi chercher depuis **⚙ › Mise à jour**. Un clic l'installe et relance l'app.

Chaque version est signée par Koredge : l'app refuse une mise à jour dont la signature ou le contenu ne correspond pas. Le dossier de l'app doit être modifiable par toi : **Applications** sur Mac, ton dossier personnel sous Windows et Linux.

## Problèmes fréquents

- **Aucune session n'apparaît** : l'app lit les sessions de la machine où elle tourne. Sous Windows, vérifie que tu as pris la version qui correspond à l'endroit où tu utilises Claude Code (voir « Avant d'installer »).
- **« claude introuvable » dans le chat** : installe Claude Code, connecte-toi, et vérifie que `claude` répond dans un terminal. Relance ensuite l'app.
