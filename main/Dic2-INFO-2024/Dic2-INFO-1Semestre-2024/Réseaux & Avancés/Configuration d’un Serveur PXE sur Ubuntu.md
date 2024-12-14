

---

# Introduction

Le PXE, ou` Preboot eXecution Environment`, est une technologie qui permet à une machine de démarrer directement via le réseau, sans système d’exploitation installé localement.

Il repose sur plusieurs composants essentiels :

- **DHCP** : Attribue une adresse IP et indique où trouver les fichiers nécessaires.
- **TFTP** : Transfère les fichiers de démarrage tels que le bootloader.
- **Bootloader** : Charge ensuite un système d’exploitation ou une image Linux minimaliste.

Dans ce rapport, nous expliquerons les concepts fondamentaux du PXE et fournirons un guide complet pour mettre en place une infrastructure PXE sur un réseau local. Une démonstration pratique sera également présentée.

---

# Présentation des concepts PXE

### **DHCP (Dynamic Host Configuration Protocol)**

Le **DHCP** est un protocole réseau qui simplifie l’attribution automatique des adresses IP et d’autres paramètres réseau aux appareils.

## Fonctionnement du DHCP

Le DHCP suit quatre étapes principales :

1. **Découverte (Discover)** : La machine cliente envoie une requête pour signaler qu’elle a besoin de paramètres réseau.
2. **Offre (Offer)** : Le serveur DHCP répond avec une offre contenant une adresse IP disponible et les paramètres réseau.
3. **Demande (Request)** : La machine cliente confirme l’acceptation de l’offre reçue.
4. **Affectation (Acknowledge)** : Le serveur finalise l’attribution de l’adresse IP.

## Avantages du DHCP

- **Automatisation** : Réduit les tâches manuelles.
- **Dynamisme** : Permet une gestion efficace des adresses IP.
- **Évolutivité** : Convient à tous types de réseaux, petits ou grands.

> **Rôle dans PXE** : Le serveur DHCP fournit non seulement une adresse IP, mais aussi l’emplacement du fichier de démarrage (bootloader).

---

# TFTP (Trivial File Transfer Protocol)

Le **TFTP** est un protocole léger utilisé pour transférer des fichiers dans des environnements simples, souvent en combinaison avec PXE.

## Caractéristiques principales

- **Protocole simple** : Basé sur UDP (pas de connexion persistante).
- **Port utilisé** : UDP 69.
- **Usage limité** : Utilisé pour des fichiers de petite taille dans des environnements contrôlés.

## Exemples d'utilisation

- Transfert de fichiers de configuration pour des équipements réseau.
- Mise à jour de micrologiciels (firmwares).
- Chargement des fichiers de démarrage lors d’un boot PXE.

## Limites du TFTP

- **Pas de sécurité** : Pas de cryptage ni d’authentification.
- **Faible flexibilité** : Convient uniquement à des cas simples.

> **Rôle dans PXE** : Le serveur TFTP transfère les fichiers nécessaires (comme `pxelinux.0` ou `vmlinuz`) à la machine cliente.

---

# Le Bootloader

Le **bootloader** est un programme clé qui amorce une machine en chargeant un système d’exploitation.

## Rôles principaux

1. **Initialisation matérielle** : Vérifie que les composants matériels (RAM, processeur) sont prêts.
2. **Chargement du noyau** : Localise et charge le noyau en mémoire.
3. **Transfert de contrôle** : Lance le système d’exploitation.

## Exemples de bootloaders

- **pxelinux** (de SYSLINUX)
- **iPXE**
- **GRUB**

> **Rôle dans PXE** : Une fois le fichier bootloader téléchargé via TFTP, il affiche un menu d’options (par ex., installer un OS ou démarrer une image live).

---

# Comment tout cela fonctionne ensemble

1. **Machine cliente sans OS** : Configurez la carte réseau pour activer le démarrage PXE.
2. **Requête DHCP** : La machine cliente demande une adresse IP et les informations pour localiser le bootloader.
3. **Téléchargement TFTP** : Le fichier `pxelinux.0` ou équivalent est téléchargé.
4. **Chargement du menu de démarrage** : Le bootloader affiche les options disponibles.
5. **Démarrage ou installation** : Les fichiers nécessaires (noyau, `initrd`, etc.) sont chargés et exécutés.

---
# Prérequis

- Un serveur sous Ubuntu Server 20 ou supérieur.
- Droits administratifs (`sudo`).
- Un réseau local (LAN).
- Fichiers d’installation ou système d’exploitation à distribuer via PXE.

---
# Étape 1 : Installer les services nécessaires

Mettez à jour le système et installez les paquets nécessaires pour le serveur PXE.

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install isc-dhcp-server tftp-hpa syslinux pxelinux
```

---

# Étape 2 : Configurer une adresse IP statique

Avant de configurer les services DHCP et TFTP, assurez vous que le serveur utilise une adresse IP statique.

## Modifier la configuration Netplan

1. Ouvrez le fichier de configuration Netplan :
    
    ```bash
    sudo nano /etc/netplan/01-netcfg.yaml
    ```
    
2. Ajoutez ou modifiez la configuration pour définir une adresse IP statique :
    
    ```yaml
    network:
      version: 2
      renderer: networkd
      ethernets:
        enp0s3:
          addresses:
            - 192.168.1.10/24
          nameservers:
            addresses:
              - 8.8.8.8
              - 8.8.4.4
    ```
    
3. Appliquez la configuration :
    
    ```bash
    sudo netplan apply
    ```
    
4. Vérifiez l’adresse IP configurée :
    
    ```bash
    ifconfig
    ```
    

---


# Étape 3 : Configurer le serveur DHCP

Le serveur DHCP attribuera les adresses IP aux clients PXE.

### **Modifier la configuration DHCP**

1. Éditez le fichier de configuration DHCP :
    
    ```bash
    sudo nano /etc/dhcp/dhcpd.conf
    ```
    
2. Ajoutez la configuration pour votre réseau :
    
    ```conf
    subnet 192.168.1.0 netmask 255.255.255.0 {
        range 192.168.1.100 192.168.1.200;
        option routers 192.168.1.1;
        option broadcast-address 192.168.1.255;
        next-server 192.168.1.10; # Adresse du serveur PXE
        filename "pxelinux.0";    # Fichier de boot
    }
    ```
    
3. Redémarrez le service DHCP :
    
    ```bash
    sudo systemctl restart isc-dhcp-server
    ```
    
4. Vérifiez le statut du service :
    
    ```bash
    sudo systemctl status isc-dhcp-server
    ```
    

---

# Étape 4 : Configurer le serveur TFTP

Le serveur TFTP sert les fichiers nécessaires au démarrage PXE.

## Configurer TFTP-HPA

1. Éditez le fichier de configuration :
    
    ```bash
    sudo nano /etc/default/tftpd-hpa
    ```
    
2. Assurez vous que les paramètres suivants sont définis :
    
    ```conf
    TFTP_USERNAME="tftp"
    TFTP_DIRECTORY="/srv/tftp"
    TFTP_ADDRESS="192.168.1.10:69"
    TFTP_OPTIONS="--secure"
    ```
    
3. Créez les dossiers nécessaires et copiez les fichiers PXELINUX :
    
    ```bash
    sudo mkdir -p /srv/tftp/pxelinux.cfg
    sudo cp /usr/lib/syslinux/modules/bios/pxelinux.0 /srv/tftp/
    ```
    
4. Copiez les fichiers `.c32` nécessaires pour les menus PXE :
    
    ```bash
    sudo cp /usr/lib/syslinux/modules/bios/*.c32 /srv/tftp/
    ```
    
5. Redémarrez le service TFTP :
    
    ```bash
    sudo systemctl restart tftpd-hpa
    ```
    

---

# Étape 5 : Configurer le bootloader PXELINUX

1. Créez le fichier de configuration PXE :
    
    ```bash
    sudo nano /srv/tftp/pxelinux.cfg/default
    ```
    
2. Ajoutez un menu simple :
    
    ```conf
    DEFAULT menu.c32
    PROMPT 0
    MENU TITLE PXE Boot Menu
    
    LABEL ubuntu
        MENU LABEL Install Ubuntu Server
        KERNEL ubuntu/vmlinuz
        APPEND initrd=ubuntu/initrd.img
    ```
    
3. Placez les fichiers nécessaires (`vmlinuz` et `initrd.gz`) dans `/srv/tftp/ubuntu` :
    
    ```bash
    sudo mkdir -p /srv/tftp/ubuntu
    sudo cp /chemin/vers/vmlinuz /srv/tftp/ubuntu/
    sudo cp /chemin/vers/initrd.gz /srv/tftp/ubuntu/
    ```
    

---

# Étape 6 : Télécharger un système d’exploitation

1. **Téléchargez les fichiers nécessaires** :  
    Rendez-vous sur le site officiel de votre système d’exploitation (par exemple Ubuntu) et récupérez les fichiers `vmlinuz` et `initrd.gz`.
    
2. Placez les dans le répertoire `/srv/tftp/ubuntu` comme indiqué précédemment.
    

---

# Étape 7 : Tester le serveur PXE

1. Configurez un client PXE (physique ou virtuel) pour démarrer sur le réseau via PXE.
    
2. Démarrez le client et vérifiez que le menu PXE s’affiche correctement.
    

---
# Remarque :
Voici une partie "Remarque" à ajouter pour clarifier certains points spécifiques concernant la configuration réseau des machines virtuelles.


## Configuration du réseau pour les machines virtuelles

- **Type de réseau** :  
    Pour que le processus PXE fonctionne correctement, les machines virtuelles (client et serveur) doivent être configurées pour utiliser un réseau **interne** sur VirtualBox. Cela garantit que les communications entre les machines se font uniquement au sein de ce réseau privé sans interférences extérieures.
    
    Voici comment configurer le réseau :
    
    1. Ouvrez les paramètres de la machine virtuelle dans VirtualBox.
    2. Accédez à l'onglet **Réseau**.
    3. Choisissez le mode **Réseau interne** (`Internal Network`) pour l'adaptateur réseau.
	    ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe5vfqYZ2xHF6U7Av5b9kuuh8doptkA6_kr2wBzzf2y5cnUDci5PVRbAWDhoxRc_P6oe9_XovLIE_xIdHUxW3ffnBiWRfWW88iRhi0vCFu8_fKxWfzwGziPo3sAtTNGKhCy8FuodDiQEKpVVE3PyvU?key=I9-v96jcWTAl66nrq8n5pehO)
- **Machine cliente** :
    
    - Lors de la configuration de la machine cliente, il est essentiel de s'assurer que le **démarrage réseau (PXE)** est activé.
    - Pour ce faire :
        1. Accédez aux paramètres de la machine cliente dans VirtualBox.
        2. Cliquez sur l'onglet **Système**, puis sur la sous-section **Ordre d'amorçage**.
        3. Cochez **Réseau** et placez le en première position dans la liste des options de démarrage. Cela garantit que la machine cliente tente d'amorcer via le réseau avant de vérifier d'autres supports comme le disque dur ou le lecteur optique.
        ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXddd4ielGLQGPvrOMlTEykHxBbNDFLcdP7BBeFiiapu00ryrdzQuWFV0ncQsmmhko89lG6defftExzXfu1-kYAOZCrl1eSqHoRqFaiLMElI5Zpb_hmj_5iBkWqBfW8zkpBv1z12TqjOCqnyoexra4Q?key=I9-v96jcWTAl66nrq8n5pehO)

## Pourquoi cette configuration ?

- En mettant en place un réseau interne, vous vous assurez que :
    
    - Le serveur DHCP et TFTP communiquent uniquement avec les clients PXE dans cet environnement isolé.
    - Il n’y a pas de conflit avec d’autres serveurs DHCP éventuellement présents sur un réseau public ou externe.
- Le fait de prioriser le démarrage réseau dans l’ordre d’amorçage de la machine cliente garantit qu’elle essaiera de se connecter au serveur PXE pour démarrer sans chercher d’autres supports.
    

---

# Conclusion
Le PXE est une technologie puissante pour déployer des systèmes rapidement sur des machines sans disque dur ou OS préinstallé. Grâce à ce guide, vous disposez d’une infrastructure PXE fonctionnelle prête à être utilisée.