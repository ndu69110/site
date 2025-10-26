---
date: 2025-10-26
authors: [squidfunk, alexvoss]
categories:
  - General
---

# [VPS Oracle] Créez votre propre serveur Cloud gratuit à vie

<!-- more -->

1 juillet 2024·12 mins·79 ·11 · Like

TutoVPSOracleServeur CloudNextCloudGratuit à vie

![JustinType](https://justintype.github.io/img/Capture.PNG)

Auteur

JustinType

Auditeur - Pentester chez  [Wavestone](https://www.wavestone.com/fr/)

-   [Introduction](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#introduction)
    -   [C’est quoi le Cloud ?](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cest-quoi-le-cloud-)
-   [Les différents types de Cloud](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#les-diff%C3%A9rents-types-de-cloud)
    -   [Cloud Public vs Cloud Privé](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cloud-public-vs-cloud-priv%C3%A9)
    -   [Cloud Hybride vs Multi Cloud](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cloud-hybride-vs-multi-cloud)
    -   [Avantages et inconvénients](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#avantages-et-inconv%C3%A9nients)
-   [Solution retenue : NextCloud](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#solution-retenue--nextcloud)
    -   [Avantages](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#avantages)
    -   [Inconvénients](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#inconv%C3%A9nients)
-   [Création du serveur Cloud](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cr%C3%A9ation-du-serveur-cloud)
    -   [Création de l’instance](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cr%C3%A9ation-de-linstance)
-   [Installation de NextCloud](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#installation-de-nextcloud)
    -   [Création du compte administrateur](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cr%C3%A9ation-du-compte-administrateur)
    -   [Réglage du domaine de confiance](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#r%C3%A9glage-du-domaine-de-confiance)
-   [Configuration de NextCloud](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#configuration-de-nextcloud)
    -   [Certificat SSL/TLS avec Let’s Encrypt](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#certificat-ssltls-avec-lets-encrypt)
    -   [Certificat SSL/TLS auto-signé](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#certificat-ssltls-auto-sign%C3%A9)
    -   [Configuration du pare-feu](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#configuration-du-pare-feu)
-   [Utilisation de NextCloud](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#utilisation-de-nextcloud)
    -   [Vérifiez l’espace de stockage](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#v%C3%A9rifiez-lespace-de-stockage)
    -   [Créer des utilisateurs](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cr%C3%A9er-des-utilisateurs)
    -   [Accéder à son serveur depuis son smartphone](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#acc%C3%A9der-%C3%A0-son-serveur-depuis-son-smartphone)
    -   [Applications](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#applications)
-   [Conclusion](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#conclusion)

VPS Oracle - Cet article fait partie d'une série.

[Partie 0: [VPS Oracle] Introduction de l'offre Cloud d'Oracle](https://justintype.github.io/fr/posts/oracle_presentation/)

[Partie 1: [VPS Oracle] Créez votre propre serveur Minecraft gratuit à vie](https://justintype.github.io/fr/posts/oracle_minecraft_server/)

[Partie 2: [VPS Oracle] Créez votre propre serveur VPN gratuit à vie](https://justintype.github.io/fr/posts/oracle_openvpn_server/)

Partie 3: Cet article

## Introduction[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#introduction)

Cet article fait partie d’une série consacrée à l’hébergement de services gratuits à vie sur un serveur privé. Dans celui-ci je vous présente comment  **créer votre propre serveur Cloud.**

### C’est quoi le Cloud ?[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cest-quoi-le-cloud-)

On entend souvent parler de ce terme sans forcément comprendre ce qui se cache derrière. En réalité c’est assez simple !

> Le cloud est un ensemble de services informatiques accessibles via Internet.

Au lieu d’utiliser des logiciels et du stockage sur votre propre ordinateur, vous utilisez les serveurs d’autres entreprises qui détiennent ces ressources.

Ces services sont fournis par des entreprises spécialisées comme :

-   Amazon Web Services (AWS)
-   Google Cloud
-   Oracle Cloud Infrastructure (OCI)
-   Microsoft Azure
-   OVH
-   …

Pour Google Cloud par exemple :

Au lieu d’installer Word, Excel, PowerPoint et de stocker tous vos fichiers sur votre ordinateur vous utilisez les serveurs de Google sur lesquels vous avez un certain espace de stockage réservé et où tous ces logiciels sont déjà installés.

En une phrase simple : “**Le Cloud c’est utiliser les ressources de quelqu’un d’autre à distance**”

![matrix](https://justintype.github.io/fr/posts/oracle_nextcloud_server/matrix.png)

## Les différents types de Cloud[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#les-diff%c3%a9rents-types-de-cloud)

Bien que le principe reste le même, il existe différents types de Clouds

### Cloud Public vs Cloud Privé[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cloud-public-vs-cloud-priv%c3%a9)

**Un cloud public est un service offert à plusieurs clients par un même fournisseur**. Les clients se partagent les ressources du fournisseur. Même si les clients ne voient que leurs propres données, en réalité les données de chaque client sont stockés au même endroit.

Tous les clients utilisent le même “ordinateur” mais chacun à son dossier réservé en quelque sorte.

À l’opposé,  **le cloud privé est un service qui n’est partagé avec aucune autre organisation**. L’utilisateur du cloud privé a le cloud pour lui seul.

Dans ce cas le client utilise un ordinateur qui lui est réservé mais qui ne lui appartient pas.

![public_vs_private_clouds](https://justintype.github.io/fr/posts/oracle_nextcloud_server/public_vs_private_clouds.png)

### Cloud Hybride vs Multi Cloud[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cloud-hybride-vs-multi-cloud)

Le  **cloud hybride**  peut se définir comme  **un environnement composé de plusieurs clouds connectés entre eux**. Il peut s’agir de plusieurs clouds publics, privés, ou d’un mélange des deux. Le cloud public peut être utilisé pour certaines tâches, et le cloud privé pour d’autres.

Souvent confondu avec le cloud hybride,  **le multi cloud s’appuie sur des services cloud différents émanant de plusieurs prestataires**.

Tous les clouds hybrides sont par définition des multiclouds, même si l’inverse n’est pas toujours vrai.

![multi_vs_hybride_clouds](https://justintype.github.io/fr/posts/oracle_nextcloud_server/multi_vs_hybrid_cloud.png)

### Avantages et inconvénients[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#avantages-et-inconv%c3%a9nients)

**Un cloud public est généralement moins couteux et plus simple à gérer**  car c’est le fournisseur qui s’occupe d’installer les logiciels, de les paramétrer, de les mettre à jour…

**En revanche cela peut poser des soucis de sécurité**, en effet si un client du fournisseur se fait pirater et que les attaquants obtiennent tous les accès au serveur, ils seront alors en mesure de voler vos données puisqu’elles se trouvent au même endroit !

> Un cloud public c’est donc un gain de temps et d’argent mais au détriment de la sécurité

**Au contraire un cloud privé est plus sécurisé**  car vous êtes le seul utilisateur de votre espace, mais cela coûte généralement plus cher et c’est à vous de faire l’installation, la configuration et la mise à jour des logiciels.

Un particulier souhaitant simplement stocker quelques photos de vacances qu’il va publier sur les réseaux sociaux se satisfera amplement d’un cloud public, là où une entreprise avec des données sensibles se tournera plutôt vers un cloud privé.

Comme toujours cela dépend donc de vos besoins ! Chaque problème à sa solution.

![problem_solving](https://justintype.github.io/fr/posts/oracle_nextcloud_server/problem_solving.png)

> Cependant ne croyez pas que les clouds privés soient uniquement réservés aux entreprises !

En effet si vous souhaitez stocker des mots de passe, des documents de travail sur des projets personnels, partager des documents privés à certaines personnes uniquement, etc. alors le cloud privé peut vous intéresser.

> Et ça tombe bien c’est ce que nous allons faire en créant notre propre serveur privé !

## Solution retenue : NextCloud[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#solution-retenue--nextcloud)

Nextcloud est une solution de stockage et de partage de fichiers en ligne installable sur son propre serveur.

### Avantages[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#avantages)

-   Il est **open-source,** cela veut dire que son code source est disponible publiquement. Il y a amélioration continue du logiciel car n’importe qui peut contribuer au code.
-   Il dispose d’une **grande communauté**, ce qui garantie des mises à jour régulières et une documentation importante.
-   Il dispose de nombreuses  **applications**  qui permettent de transformer son cloud en gestionnaire de mots de passe (comme BitWarden), serveur de musique (comme Spotify), serveur de visioconférence (comme Teams), et bien d’autres.
-   Il est **multi-plateforme**, ce qui permet de l’utiliser simplement sur Windows, MacOS, Linux, Android ou iOS.
-   Il est **gratuit à vie !**

### Inconvénients[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#inconv%c3%a9nients)

-   Nécessite d’installer et de configurer l’application  **soi-même**
-   **200 Go de stockage gratuit maximum**  (limité par l’offre “Always Free” d’OCI)

En comparaison vous disposez de 15 Go gratuit chez Google et de 5 Go chez Apple.

> Bien, maintenant que vous savez tout, commençons !

## Création du serveur Cloud[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cr%c3%a9ation-du-serveur-cloud)

Il est fortement conseillé de lire l’introdution de la série, car j’y présente l’offre “**Always Free**” d’OCI que nous allons utiliser. Des notions comme la création d’une VM, l’allocation de ses ressources, comment y accéder, transférer des fichiers, configurer son firewall, etc, y ont été abordées.

![Thumbnail Oracle Minecraft Server](https://justintype.github.io/fr/posts/oracle_nextcloud_server/oracle_presentation.png)

[→ Lire l'introduction de la série](https://justintype.github.io/fr/posts/oracle_presentation/)

### Création de l’instance[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cr%c3%a9ation-de-linstance)

Pour commencer, nous allons devoir créer une instance sur OCI.

Choisissez un nom de serveur, laissez le compartiment par défaut et changez l’image :

![instance1](https://justintype.github.io/fr/posts/oracle_nextcloud_server/instance1.png)

Choisissez l’image  **Ubuntu 20.04**  :

![instance2](https://justintype.github.io/fr/posts/oracle_nextcloud_server/instance2.png)

Choisissez les ressources à allouer :

![instance3](https://justintype.github.io/fr/posts/oracle_nextcloud_server/instance3.png)

Attention à ne pas dépasser vos ressources “Always Free” si vous disposez d’autres instances !

Vous pouvez changer de VNIC ou laisser celui par défaut, puis téléchargez la clé privée SSH :

![instance4](https://justintype.github.io/fr/posts/oracle_nextcloud_server/instance4.png)

Créez un boot volume de la taille voulue, ici je prends le maximum donc  **200 Go**  :

![instance5](https://justintype.github.io/fr/posts/oracle_nextcloud_server/instance5.png)

Laissez le reste et créez l’instance :

![instance6](https://justintype.github.io/fr/posts/oracle_nextcloud_server/instance6.png)

Une fois l’instance créée, notez bien l’adresse IP de votre VM :

![instance7](https://justintype.github.io/fr/posts/oracle_nextcloud_server/instance7.png)

Adresse IP modifiée

Connectez vous à votre VM via SSH :

```bash
ssh ubuntu@[IP_de_votre_VM] -i [cle_ssh]

```

Puis faites les mises à jour système :

```bash
sudo apt update -y && sudo apt upgrade -y

```

Votre instance est prête, nous allons maintenant installer NextCloud.

## Installation de NextCloud[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#installation-de-nextcloud)

Installez le paquet nextcloud via  `snap`  :

```bash
sudo snap install nextcloud

```

### Création du compte administrateur[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cr%c3%a9ation-du-compte-administrateur)

Créez un nouveau compte administrateur avec la commande suivante, ce compte sera utilisé pour paramétrer NextCloud :

```bash
sudo nextcloud.manual-install [compte] [mot_de_passe]

```

Le message suivant indique que Nextcloud a été configuré correctement :

```
Nextcloud was successfully installed

```

### Réglage du domaine de confiance[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#r%c3%a9glage-du-domaine-de-confiance)

Lors de l’installation en ligne de commande, NextCloud limite les noms d’hôtes auxquels l’instance répondra.

Par défaut, NextCloud n’autorise que  **`localhost`**  comme domaine de confiance, or nous ne pourrons pas accéder à ce domaine depuis l’extérieur, nous allons donc ajouter l’adresse IP du serveur comme domaine de confiance.

Vous pouvez consulter les paramètres actuels en interrogeant la valeur du tableau **`trusted_domains`** :

```bash
sudo nextcloud.occ config:system:get trusted_domains

```

![trusted_domain1](https://justintype.github.io/fr/posts/oracle_nextcloud_server/trusted_domain1.png)

Actuellement, seul **`localhost`** est présent comme valeur dans le tableau. Nous pouvons ajouter l’adresse IP de notre serveur en tapant :

```bash
sudo nextcloud.occ config:system:set trusted_domains 1 --value=[IP_de_votre_VM]

```

Pour ceux qui détiennent un nom de domaine, vous pouvez remplacer l’adresse IP de votre VM par ce nom de domaine.

![trusted_domain2](https://justintype.github.io/fr/posts/oracle_nextcloud_server/trusted_domain2.png)

Si nous interrogeons à nouveau les domaines de confiance, nous constatons que nous avons bien l’adresse IP de notre VM :

```bash
sudo nextcloud.occ config:system:get trusted_domains

```

![trusted_domain3](https://justintype.github.io/fr/posts/oracle_nextcloud_server/trusted_domain3.png)

Vous pouvez ajouter d’autres adresses IP ou domaines avec la commande `config:system:set`, il faudra simplement incrémenter le numéro → exemple pour un deuxième domaine :  `sudo nextcloud.occ config:system:set trusted_domains 2 --value=deuxieme_domaine.com`

## Configuration de NextCloud[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#configuration-de-nextcloud)

Actuellement notre serveur NextCloud est bien paramétré pour faire confiance à un nom de domaine ou une adresse IP. Cependant aucun processus de chiffrement n’a été configuré.

> Vous savez le petit cadenas qui indique que vous êtes bien en  **HTTPS.**

![https](https://justintype.github.io/fr/posts/oracle_nextcloud_server/https.png)

Si on s’arrête là les données transmises à votre serveur cloud seront en clair sur le réseau et on veut éviter ça !

Pour cela on va mettre en place un  **certificat SSL/TLS.**

### Certificat SSL/TLS avec Let’s Encrypt[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#certificat-ssltls-avec-lets-encrypt)

Cette solution est destinée aux personnes possédant un nom de domaine, si ce n’est pas votre cas, suivez les indications pour le certificat auto-signé.

Si vous avez un nom de domaine associé à votre serveur NextCloud, la meilleure option pour sécuriser votre interface web est d’obtenir un certificat Let’s Encrypt.

[Let’s Encrypt](https://letsencrypt.org/fr/how-it-works/)  est une autorité de certification gratuite, automatisée et mise à votre disposition par la société d’utilité publique Internet Security Research Group (ISRG).

Demandez un certificat Let’s Encrypt en tapant :

```bash
sudo nextcloud.enable-https lets-encrypt

```

Il vous sera d’abord demandé si votre serveur remplit les conditions nécessaires pour demander un certificat au service Let’s Encrypt :

```
In order for Let's Encrypt to verify that you actually own the
domain(s) for which you're requesting a certificate, there are a
number of requirements of which you need to be aware:

1. In order to register with the Let's Encrypt ACME server, you must
   agree to the currently-in-effect Subscriber Agreement located
   here:

       https://letsencrypt.org/repository/

   By continuing to use this tool you agree to these terms. Please
   cancel now if otherwise.

2. You must have the domain name(s) for which you want certificates
   pointing at the external IP address of this machine.

3. Both ports 80 and 443 on the external IP address of this machine
   must point to this machine (e.g. port forwarding might need to be
   setup on your router).

Have you met these requirements? (y/n)

```

→ Tapez `y` pour continuer.

Ensuite, il vous sera demandé de fournir une adresse électronique à utiliser pour les opérations de récupération :

```
Please enter an email address (for urgent notices or key recovery):

```

→ Entrez votre adresse électronique et appuyez sur la touche `Enter` pour continuer.

Enfin, entrez le nom de domaine associé à votre serveur NextCloud :

```
Please enter your domain name(s) (space-separated): example.com

```

Votre certificat Let’s Encrypt sera demandé et, si tout s’est bien passé, l’instance interne d’Apache sera redémarrée pour mettre immédiatement en œuvre le SSL :

```
Attempting to obtain certificates... done
Restarting apache... done

```

Vous pouvez maintenant passer à l’étape de configuration du pare-feu NextCloud.

### Certificat SSL/TLS auto-signé[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#certificat-ssltls-auto-sign%c3%a9)

Si vous ne disposez  _**pas de nom de domaine**_, vous pouvez quand même mettre en place du chiffrement sur votre serveur Nextcloud en générant  **un certificat SSL/TLS auto-signé**. Ce certificat permettra d’accéder à l’interface web via une connexion chiffrée.

Votre navigateur affichera probablement un avertissement lorsque vous essayerez de vous connecter à l’interface web, c’est normal car il ne peut pas vérifier l’identité de votre serveur.

Pour générer un certificat auto-signé et l’utiliser sur votre serveur Nextcloud tapez :

```bash
sudo nextcloud.enable-https self-signed

```

![self_signed](https://justintype.github.io/fr/posts/oracle_nextcloud_server/self_signed.png)

La sortie ci-dessus indique que NextCloud a généré et activé un certificat auto-signé.

Vous pouvez maintenant passer à l’étape de configuration du pare-feu NextCloud.

### Configuration du pare-feu[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#configuration-du-pare-feu)

De base, l’image Ubuntu d’OCI est paramétrée avec  `iptables`, le paramétrage bloque l’accès aux ports  **80**  et  **443**  (ports utilisés par les protocoles HTTP et HTTPS).

Nous allons remplacer ce paramétrage avec le pare-feu  `ufw`  et ouvrir ces ports.

Tout d’abord exécutez les commandes suivantes :

```bash
sudo iptables -P INPUT ACCEPT
sudo iptables -P OUTPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -F

```

Puis autorisez le pare-feu  `ufw`  avec la commande :

```bash
sudo ufw enable

```

Vous pouvez vérifier si  `ufw`  est actif avec la commande :

```bash
sudo ufw status

```

Enfin autorisez le protocole SSH ainsi que les ports 80 et 443 :

```bash
sudo ufw allow ssh
sudo ufw allow 443/tcp
sudo ufw allow 80/tcp

```

Vous pouvez vérifier les règles du pare-feu avec la commande :

```bash
sudo ufw status numbered

```

![firewall1](https://justintype.github.io/fr/posts/oracle_nextcloud_server/firewall1.png)

Vous n’avez plus qu’à ouvrir ces ports sur le VNIC d’OCI :

![firewall2](https://justintype.github.io/fr/posts/oracle_nextcloud_server/firewall2.png)

→ Votre serveur Nexcloud est prêt à être utilisé !

## Utilisation de NextCloud[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#utilisation-de-nextcloud)

Rendez-vous sur l’url  `https://[IP_de_votre_VM]`  et connectez-vous avec le compte administrateur précédemment créé :

![utilisation1](https://justintype.github.io/fr/posts/oracle_nextcloud_server/utilisation1.png)

Pour chaque nouvel utilisateur, NextCloud créer des fichiers “templates”, ceux-ci servent à donner des exemples d’utilisation mais vous pouvez tout à fait les supprimer.

### Vérifiez l’espace de stockage[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#v%c3%a9rifiez-lespace-de-stockage)

Rendez-vous dans “_**Paramètres d’administration > Système**_” pour vérifier l’espace de stockage disponible sur votre serveur :

![utilisation2](https://justintype.github.io/fr/posts/oracle_nextcloud_server/utilisation1.png)

![utilisation3](https://justintype.github.io/fr/posts/oracle_nextcloud_server/utilisation3.png)

### Créer des utilisateurs[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#cr%c3%a9er-des-utilisateurs)

Rendez-vous dans l’onglet “_**Utilisateurs**_” :

![utilisation4](https://justintype.github.io/fr/posts/oracle_nextcloud_server/utilisation4.png)

Puis cliquez sur “_**Nouveau compte**_” et renseignez les informations du nouveau compte :

![utilisation5](https://justintype.github.io/fr/posts/oracle_nextcloud_server/utilisation5.png)

Vous pouvez choisir le stockage réservé a cet utilisateur.

L’utilisateur peut désormais se connecter et stocker des fichiers sur votre serveur NextCloud :

![utilisation6](https://justintype.github.io/fr/posts/oracle_nextcloud_server/utilisation6.png)

![utilisation7](https://justintype.github.io/fr/posts/oracle_nextcloud_server/utilisation1.png)

Vous pouvez partager les accès à vos amis ou votre famille tout en affinant les paramètres de chacun. Il est possible par exemple de n’autoriser que le stockage de photos ou de vidéos, d’indiquer l’espace de stockage réservé à chacun, etc.

Pour plus d’informations :  [Documentation NextCloud](https://docs.nextcloud.com/)

### Accéder à son serveur depuis son smartphone[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#acc%c3%a9der-%c3%a0-son-serveur-depuis-son-smartphone)

Vous pouvez accéder à votre serveur NextCloud depuis n’importe quel navigateur via l’url  `https://[IP_de_votre_VM]`  ou bien vous pouvez installer  **l’application mobile**  NextCloud sur votre smartphone.

Il vous suffira de renseigner l’url de votre serveur :

![smartphone1](https://justintype.github.io/fr/posts/oracle_nextcloud_server/smartphone1.png)

Puis de vous connecter pour accéder à tous vos fichiers :

![smartphone2](https://justintype.github.io/fr/posts/oracle_nextcloud_server/smartphone2.png)

### Applications[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#applications)

Vous pouvez également installer des applications depuis l’onglet “_**Applications**_” :

![apps1](https://justintype.github.io/fr/posts/oracle_nextcloud_server/apps1.png)

![apps2](https://justintype.github.io/fr/posts/oracle_nextcloud_server/apps2.png)

NextCloud possède de nombreuses applications écrites par la communauté, voici quelques exemples :

-   **`Audio Player`**  → pour stocker et jouer des musiques (comme Spotify)
-   **`Only Office`**  → pour éditer des fichiers word, excel, powerpoint simultanément (comme Google Drive)
-   **`Passwords`**  → pour stocker et gérer vos mots de passe (comme BitWarden)
-   **`Talk`**  → pour réaliser des appels audios et vidéos (comme Teams)
-   **`Calendar`**  → pour gérer vos calendriers (comme Google Agenda ou Outlook)
-   **`Notes`**  → pour gérer vos notes en ligne avec le langage markdown (comme Notion)

Vous pouvez retrouver toutes les applications disponibles ici :  [NextCloud App Store](https://apps.nextcloud.com/)

## Conclusion[#](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#conclusion)

Dans cet article, je vous ai présenté comment créer votre propre serveur Cloud gratuit à vie avec la solution NextCloud, en utilisant l’offre “Always Free” d’Oracle Cloud Infrastructure.

L’objectif était de vous offrir une solution pratique et gratuite tout en vous familiarisant avec le domaine du cloud et de la sécurité informatique.

Après la lecture de cet article, vous savez désormais :

-   Ce qu’est un Cloud
-   Quels sont les différents types de Cloud
-   Comment créer votre propre Cloud gratuit à vie

J’espère que vous aurez apprécié la lecture de l’article, si c’est le cas n’hésitez pas à le liker et à le partager à vos amis ou collègues qui pourraient être intéressés !

VPS Oracle - Cet article fait partie d'une série.

[Partie 0: [VPS Oracle] Introduction de l'offre Cloud d'Oracle](https://justintype.github.io/fr/posts/oracle_presentation/)

[Partie 1: [VPS Oracle] Créez votre propre serveur Minecraft gratuit à vie](https://justintype.github.io/fr/posts/oracle_minecraft_server/)

[Partie 2: [VPS Oracle] Créez votre propre serveur VPN gratuit à vie](https://justintype.github.io/fr/posts/oracle_openvpn_server/)

Partie 3: Cet article

[↑](https://justintype.github.io/fr/posts/oracle_nextcloud_server/#the-top "Remonter en haut de la page")

Copyright 2025 © Valentin Thirion. Tous droits réservés.

![Buy Me A Coffee](https://cdn.buymeacoffee.com/widget/assets/coffee%20cup.svg)