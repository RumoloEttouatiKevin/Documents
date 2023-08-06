# Installation d'une VM Ubuntu 22.04 avec VirtualBox 7.0.10

## 1. Téléchargements

- `VirtualBox` => [lien](https://www.virtualbox.org/)
- `ISO Linux Ubuntu` => [lien](https://ubuntu.com/download/desktop)

## 2. Création et configuration de la VM

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
7. Sélectionner la VM et cliquer sur **Configuration**
8. Général
   1. Avancé
      1. Sélectionner **Bidirectionnel** pour *Presse-papiers partagé* et *Glisser-Déposer* pour les activer entre l'hôte et la VM
9. Affichage
   1. Écran
      1. Choisir le maximum de **Mémoire Vidéo** (**128Mo**)
      2. Choisir le nombre d'écrans possible (**2**)
10. Dossiers partagés
    1. Ajouter un dossier partagé avec l'hôte
       1. Sélectionner le chemin du dossier à partager
       2. Sélectionner **Lecture seule** et **Montage automatique**

## 3. Installation de Ubuntu

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

## 4. Configuration de la VM et de Linux

1. Cliquer sur l'onglet **Périphériques** de la VirtualBox puis cliquer sur **Insérer l'image CD des Additions invité...**
   1. Ouvrir le périphérique depuis le menu de gauche
   2. Clic droit sur **autorun.sh** et cliquer sur **Exécuter comme un programme**
2. Redémarrer la VM
3. Activer les dossiers partagés
   1. `sudo usermod -G vboxsf -a $USER`

## 5. Mise à jour du système Linux

1. `sudo apt-get update`
2. `sudo apt-get dist-upgrade`

## 6. Installation de VIM

1. Supprimer VIM tiny
   1. `sudo apt-get remove vim-tiny`
2. Installer VIM
   1. `sudo apt-get install vim`

## 7. Installation de Google Chrome

1. Installer les dépôts
   1. `sudo sh -c 'echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list'`
   2. `wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -`
2. Installer Google Chrome
   1. `sudo apt-get update`
   2. `sudo apt-get install google-chrome-stable`
3. Création d'un alias pour l'exécution
   1. Ouvrir le fichier de configuration shell de l'utilisateur courant
      1. `vi ~/.bashrc`
   2. Insérer les lignes suivantes en bas du fichier :

      ```s
      # Alias perso
      alias chrome='google-chrome'
      ```

   3. Recharger la source de la configuration
      1. `source ~/.bashrc`

## 8. Installation de VS Code

1. Installer les dépôts
   1. `wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg`
   2. `sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg`
   3. `sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'`
   4. `rm -f packages.microsoft.gpg`
2. Installer VS Code
   1. `sudo apt-get install apt-transport-https`
   2. `sudo apt-get update`
   3. `sudo apt-get install code`
3. Exécuter VS Code via la commande `code` ou `code {path/to/folder}`
   1. Si l'on souhaite récupérer sa configuration synchronisée avec Microsoft
   2. Dans le menu **Accounts** en bas à gauche
   3. Sélectionner **Turn on Settings Sync**
   4. Cocher ce que l'on souhaite synchroniser
   5. Cliquer ensuite sur **Sign in & Turn on** choisir entre GitHub ou Microsoft

## 9. Installation de Git

1. Installer Git
   1. `sudo apt-get install git`
2. Configuration de la clé SSH
   1. `ssh-keygen -C "adresse-email@exemple.fr"`
   2. `cat ~/.ssh/id_rsa.pub`
   3. Copier la clé et la saisir sur GitHub / GitLab / Azure DevOps / BitBucket ...
   4. `eval "$(ssh-agent -s)"`
   5. `ssh-add ~/.ssh/id_rsa`
   6. `git config --global user.name "Username"`
   7. `git config --global user.email "votre-email@exemple.fr"`
   8. `git config --global core.editor vim`
   9. `git config --global color.ui true`

## 10. Installation de Docker

1. Installation des paquets prérequis
   1. `sudo apt install apt-transport-https ca-certificates curl software-properties-common`
2. Installation des clés GPG et ajout aux sources APT
   1. `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg`
   2. `echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`
   3. `sudo apt-get update`
3. Installation de Docker
   1. `sudo apt-get install docker-ce`
4. Ajouter l'utilisateur courant au groupe **docker**
   1. `sudo usermod -aG docker ${USER}`
5. Recharger l'utilisateur courant ou ouvrir un nouveau terminal
   1. `su - ${USER}`

## 11. Apache Mysql PHP

<!-- TODO -->
IN PROGRESS !!!

## 12. Divers utilitaires

1. `sudo apt-get install make dkms build-essential`

## 13. Nettoyage du système

1. `sudo apt-get autoremove`
2. `sudo apt-get autoclean`
