# Installation de Ubuntu 22.04 avec WSL 2 (Windows System for Linux)

## 1. Installation de Ubuntu avec WSL

1. Ouvrir un terminal PowerShell et lancer la commande d'installation d'Ubuntu
   1. `wsl --install Ubuntu`
2. Saisir son identifiant d'utilisateur pour Linux (**krum**)
3. Saisir un mot de passe pour cet utilisateur (il est généralement demandé lors de commande `sudo`)

## 2. Exécution de WSL

1. WSL/Ubuntu peut être lancé de deux manières :
   1. Via l'application **wsl**
   2. Depuis une console (PowerShell ou l'invite de commande) avec la commande `wsl`
2. WSL/Ubuntu peut être arrêté de plusieurs manières :
   1. Depuis Linux avec la commande `sudo shutdown` programme l'arrêt du système une minute après (valeur paramétrable)
   2. Depuis Linux avec la commande `sudo poweroff` effectue l'arrêt immédiat
   3. Depuis PowerShell avec la commande `wsl --shutdown` effectue l'arrêt immédiat
3. Voir toutes les commandes possibles de WSL via un PowerShell et la commande `wsl --help`

## 3. Mise à jour du système Linux

1. `sudo apt-get update`
2. `sudo apt-get dist-upgrade`

## 4. Installation de VIM

1. Supprimer VIM tiny
   1. `sudo apt-get remove vim-tiny`
2. Installer VIM
   1. `sudo apt-get install vim`

## 5. Installer de Google Chrome

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

## 6. Installer de VS Code Server

1. S'assurer d'avoir VS Code d'installer sur l'hôte.
2. Depuis Linux via WSL se placer dans un dossier quelconque ou dans un projet et lancer la commande `code .` cette commande est détecté par l'hôte puis installe le serveur permettant la communication de VS Code à WSL et enfin le VS Code de l'hôte s'ouvre dans le projet.
3. Certaines extensions doivent être réinstallées spécifiquement pour WSL, voir l'onglet extension puis checker celle qui sont installé en LOCAL et sur WSL.

## 7. Installation de Git

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

## 8. Installation de Docker

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

## 9. Divers utilitaires

1. `sudo apt-get install build-essential`

## 10. Nettoyage du système

1. `sudo apt-get autoremove`
2. `sudo apt-get autoclean`
