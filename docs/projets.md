# Première installation d’Ubuntu Server 24.04 : outils et paquets essentiels à installer

## 1. Paquets et outils fondamentaux

Lors de la première prise en main d’**Ubuntu Server 24.04**, il est crucial d’installer et de configurer certains paquets et outils afin d’assurer la sécurité, la facilité d’administration et la maintenance du système. Voici une liste explicite et détaillée des éléments à ne pas négliger :

- **sudo**  
  Permet à un utilisateur d’exécuter des commandes avec des privilèges administrateur. Si non installé par défaut, il se configure ainsi :
  
  ```bash
  sudo apt update
  sudo apt install sudo
  usermod -aG sudo <votre_nom_utilisateur>
  ```

![enter image description here](https://www.ndu69.com/Screenshots/screenshot_2025-10-03_08-20-02.jpg)

- **openssh-server**  
  Requis pour la connexion distante au serveur en SSH. Il est généralement proposé durant l’installation ; sinon :
  
  ```bash
  sudo apt install openssh-server
  systemctl enable ssh
  systemctl start ssh
  ```

- **parted**  
  Permet l'utilisation de disque externe de plus de 2 To :
  
  ```bash
  sudo apt install parted
  ```

![enter image description here](https://www.ndu69.com/Screenshots/screenshot_2025-09-27_11-23-34.jpg)

- **net-tools**  
  Permet l'utilisation de la commande `ifconfig`, dépréciée au profit de `ip a`  :
  
  ```bash
  sudo apt install net-tools
  ```

![enter image description here](https://www.ndu69.com/Screenshots/screenshot_2025-09-27_10-06-22.jpg)

- **ufw** (Uncomplicated Firewall)  
  Facilite la gestion du pare-feu pour sécuriser le serveur. Exemple d’activation :
  
  ```bash
  sudo apt install ufw
  ufw allow OpenSSH
  ufw enable
  ufw status
  ```

- **nano**  
  Editeurs de texte essentiels pour modifier des fichiers de configuration rapidement.
  
```bash
sudo apt install nano -y
```

![enter image description here](https://www.ndu69.com/Screenshots/screenshot_2025-09-27_09-13-17.jpg)

- **htop**  
  Pour la supervision des ressources système en temps réel (CPU, RAM, processus).
  
  ```bash
  sudo apt install htop -y
  ```

- **curl** et **wget**  
  Utilitaires pour transférer des fichiers sur internet et tester la connectivité réseau.
  
  ```bash
  sudo apt install curl wget -y
  ```

- **fail2ban**  
  Protection contre les tentatives de connexion SSH bruteforce.
  
  ```bash
  sudo apt install fail2ban -y
  sudo systemctl enable fail2ban
  sudo systemctl start fail2ban
  ```

## 2. Recommandations complémentaires

- Mettre à jour le système après installation :
  
  ```bash
  sudo apt update -y
  sudo apt upgrade -y
  ```

- Installer les outils de diagnostic disque si besoin (**duf**, **ncdu**…) pour la gestion de l’espace :
  
  ```bash
  sudo apt install duf ncdu -y
  ```

![enter image description here](https://www.ndu69.com/Screenshots/screenshot_2025-09-27_09-55-32.jpg)

---

## 3. Configuration de base après installation

- Modification du mot de passe du compte root si besoin :
  
  ```bash
  sudo passwd root
  ```

![enter image description here](https://www.ndu69.com/Screenshots/screenshot_2025-09-27_09-56-43.jpg)

- Configurer les mises à jour automatiques :
  
  ```bash
  sudo apt install unattended-upgrades -y
  sudo dpkg-reconfigure unattended-upgrades
  ```

---

## 4. Bonnes pratiques

- **Sécuriser l’accès SSH** : changer le port, désactiver l’accès root direct.
- **Sauvegardes** : automatiser la sauvegarde des fichiers et bases de données.
- **Documentation** : conserver un journal des commandes utilisées pour faciliter la maintenance.

> Ces étapes garantissent une base solide, sécurisée et facilement administrable pour Ubuntu Server 24.04.

---