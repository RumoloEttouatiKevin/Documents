# Installation d'une VM Linux avec un environnement de dev

## 1. Téléchargements

- `VirtualBox` => [lien](https://www.virtualbox.org/)
- `ISO Linux Ubuntu` => [lien](https://ubuntu.com/download/desktop)

## 2. Création de la VM

1. Dans VirtualBox, cliquer sur **Nouvelle**
2. Basculer en mode expert
3. Name and Operating System
   1. Saisir un nom (**Ubuntu 22.04**)
   2. Sélectionner l'image ISO
   3. Sélectionner le type d'os (**Linux**)
   4. Sélectionner la version d'os (**Ubuntu 22.04 LTS (Jammy Jellyfish) (64-bit)**)
   5. Sélectionner **Skip Unattended Installation**
4. Hardware
   1. Choisir la quantité de RAM, minimum 4Go, attention de ne pas dépasser la zone verte (**8192Mo**)
   2. Choisir la quantité de CPU, minimum 1, attention de ne pas dépasser la zone verte (**4**)
5. Hard Disk
    1. Choisir **Create a Virtual Hard Disk Now**
    2. Choisir la taille du disque virtuel, 25Go recommandé (**50Go**)
    3. Choisir **VDI (VirtualBox Disk Image)**
6. Terminer la création

## 3. Configurer la VM

1. Sélectionner la VM et cliquer sur **Configuration**
2. Général
   1. Avancé
      1. Sélectionner **Bidirectionnel** pour *Presse-papiers partagé* et *Glisser-Déposer* pour les activer entre l'hôte et la VM
3. Affichage
   1. Écran
      1. Choisir le maximum de **Mémoire Vidéo** (**128Mo**)
      2. Choisir le nombre d'écrans possible (**2**)
4. Dossiers partagés
   1. Ajouter un dossier partagé avec l'hôte
      1. Sélectionner le chemin du dossier à partager
      2. Sélectionner **Lecture seule** et **Montage automatique**

## 4. Installer Ubuntu

1. Sélectionner la VM et cliquer sur **Démarrer**
2. Sélectionner **Try or Install Ubuntu**
3. Sélectionner la langue puis **Installer Ubuntu**
4. Choisir la disposition du clavier (**French - French (AZERTY)**)
5. Choisir **Installation minimale**
6. Laisser **Télécharger les mises à jour pendant l'installation de Ubuntu**
7. Laisser **Effacer le disque et installer Ubuntu**
8. Sélectionner le fuseau horaire
9. Saisir un nom (**Ubuntu 22.04**)
10. Saisir un nom de machine (**ubuntu2204-VirtualBox**)
11. Saisir un nom d'utilisateur (**totoKevDev**)
12. Saisir un mot de passe
13. Sélectionner **Ouvrir la session automatiquement**

## 5. Configuration de la VM

1. Cliquer sur l'onglet **Périphériques** de la VirtualBox puis cliquer sur **Insérer l'image CD des Additions invité...**
   1. Ouvrir le périphérique depuis le menu de gauche
   2. Clique droit sur **autorun.sh** et cliquer sur **Exécuter comme un programme**
   3. Reboot la VM
2. Redémarrer la VM
3. Dans un terminal
   1. `sudo apt-get update`
   2. `sudo apt-get dist-upgrade`
   3. `sudo apt-get autoremove`
   4. `sudo apt-get autoclean`
   5. `sudo apt install dkms build-essential`
4. Pour activer les dossiers partagés
   1. `sudo usermod -G vboxsf -a $USER`

## 6. Paramètres de la VM

1. Cliquer sur le menu en haut à droite puis **paramètres**
2. Naviguer dans les différents onglets pour personnaliser les paramètres
3. Redémarrer la VM

## 7. VIM

1. Supprimer VIM tiny
   1. `sudo apt-get remove vim-common vim-tiny`
2. Installer VIM
   1. `sudo apt-get install vim`

## 8. Google Chrome

1. Installer les dépôts
   1. `sudo sh -c 'echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list'`
   2. `wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -`
2. Installer Google Chrome
   1. `sudo apt-get update`
   2. `sudo apt-get install google-chrome-stable`

## 9. VSCode

1. Installer les dépôts
   1. `wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg`
   2. `sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg`
   3. `sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'`
   4. `rm -f packages.microsoft.gpg`
2. Installer VSCode
   1. `sudo apt-get install apt-transport-https`
   2. `sudo apt-get update`
   3. `sudo apt-get install code`
3. Paramétrage
   1. Dans le menu **Accounts** en bas à gauche
   2. Sélectionner **Turn on Settings Sync**
   3. Cocher ce que l'on souhaite synchroniser
   4. Cliquer ensuite sur **Sign in & Turn on** (forcer un peu si la connexion ne ce fait pas).

## 10. Git

1. Installer Git
   1. `sudo apt-get install git`
2. Configuration du compte GitHub
   1. `ssh-keygen -t ed25519 -C "votre-email@exemple.fr"`
   2. `cat ~/.ssh/id_ed25519.pub`
   3. Copier la clé et la saisir sur GitHub
   4. `eval "$(ssh-agent -s)"`
   5. `ssh-add ~/.ssh/id_ed25519`
   6. Vérifier la connexion
      1. `ssh -T git@github.com`
   7. `git config --global user.name "Username"`
   8. `git config --global user.email "votre-email@exemple.fr"`
   9. `git config --global core.editor vim`
   10. `git config --global color.ui true`

## 11. LAMP

## 12. Divers utilitaires

1. Installation de différents utilitaires
   1. `sudo apt-get install curl`
