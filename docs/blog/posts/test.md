---
date: 2025-10-26
authors: [squidfunk, alexvoss]
categories:
  - General
---

# Changer le nom d’hôte sous Ubuntu 25.04

Voici la procédure détaillée pour modifier le **hostname** (nom d'hôte) sur Ubuntu 25.04 de manière explicite et sécurisée.

---

<!-- more -->

## 1. Vérifier le nom d’hôte actuel

Ouvrez un terminal et tapez :

```bash
hostnamectl
```

Vous verrez un résultat semblable à :

```
Static hostname: serveur
Operating System: Ubuntu 25.04
```

---

## 2. Modifier le nom d’hôte avec hostnamectl

Pour changer le nom d’hôte, utilisez :

```bash
sudo hostnamectl set-hostname NOUVEAU_NOM
```

Remplacez `NOUVEAU_NOM` par le nom de votre choix.

Exemple :

```bash
sudo hostnamectl set-hostname monserveur.exemple.com
```
[1]

---

## 3. Modifier le fichier /etc/hosts

Éditez le fichier `/etc/hosts` :

```bash
sudo nano /etc/hosts
```

Trouvez la ligne qui ressemble à :

```
127.0.1.1     ancien_nom
```

Remplacez-la par :

```
127.0.1.1     monserveur.exemple.com
```

Votre fichier devrait contenir au minimum :

```
127.0.0.1   localhost
127.0.1.1   monserveur.exemple.com

# Pour IPv6 :
::1         ip6-localhost ip6-loopback
```
[1][3]

Enregistrez (`Ctrl+O`), puis quittez nano (`Ctrl+X`).

---

## 4. (Si cloud-init est installé) : Modifier cloud.cfg

Éditez le fichier `/etc/cloud/cloud.cfg` :

```bash
sudo nano /etc/cloud/cloud.cfg
```

Trouvez la ligne suivante :

```
preserve_hostname: false
```

Remplacez-la par :

```
preserve_hostname: true
```
Enregistrez et quittez.

---

## 5. Redémarrez pour appliquer définitivement

Il est recommandé de redémarrer pour s'assurer de la prise en compte complète du changement :

```bash
sudo reboot now
```

---

## Résumé des commandes principales

```bash
hostnamectl                  # Afficher le nom d’hôte actuel
sudo hostnamectl set-hostname NOUVEAU_NOM
sudo nano /etc/hosts
# (optionnel, si cloud-init) :
sudo nano /etc/cloud/cloud.cfg
sudo reboot
```

---

### Remarques

- Le nouveau nom d’hôte prend effet immédiatement pour la plupart des services, mais un redémarrage est conseillé pour éviter tout problème résiduel.
- Si vous ne modifiez pas le fichier `/etc/hosts`, vous risquez d'avoir des erreurs de résolution ("unable to resolve host").
- Utilisez toujours des noms d’hôtes conformes aux standards DNS.

---

N’hésitez pas à adapter ces instructions à vos besoins et à vérifier chaque étape.
