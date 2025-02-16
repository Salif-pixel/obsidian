---

---

---

# Cours Théorique
## **Chapitre 1 : Travail en environnement hybride et partage de ressources**

#### **Introduction**

- Les systèmes d'exploitation modernes (Windows, Linux, macOS) permettent de partager des ressources via des réseaux (Ethernet, Wi-Fi).
- Ressources partagées : dossiers, fichiers, imprimantes, modems, disques externes.
- Importance des autorisations et des règles pour sécuriser les partages, surtout pour des fichiers sensibles.

#### **Types de réseaux sous Windows**

1. **Workgroup** (pair à pair) :
    - Chaque ordinateur est indépendant.
    - Les partages sont configurés localement.
    - Peu adapté aux grandes entreprises.
2. **Domaines** :
    - Basé sur un serveur central (Active Directory Service).
    - Les utilisateurs et leurs autorisations sont centralisés sur le serveur.
    - Adapté aux environnements professionnels.

#### **Protocole SMB et Samba**

- **SMB (Server Message Block)** : Protocole utilisé par Windows pour le partage de ressources.
- **Samba** : Logiciel sous Linux permettant de partager des ressources compatibles SMB.

#### **Profils de connexion réseau (Windows)**

1. **Profil public** : Partages désactivés, pare-feu renforcé.
2. **Profil privé** : Partages activés, règles de sécurité allégées.
3. **Profil domaine** : Règles définies par le contrôleur de domaine.


#### **1.VNC et noVNC**

1. **VNC (Virtual Network Computing)** :
    
    - **Définition** : VNC est un protocole qui permet de partager un bureau graphique d'une machine à une autre à distance.
    - **Fonctionnement** :
        - Basé sur le protocole **RFB (Remote Framebuffer Protocol)**.
        - Utilisé pour accéder à une interface graphique d'une machine Linux ou Windows depuis un client.
    - **Applications** :
        - Administration de serveurs à distance.
        - Support technique.
    - **Clients populaires** : TigerVNC, RealVNC, TightVNC.
2. **noVNC** :
    
    - **Définition** : Une implémentation de VNC basée sur le web qui permet d'accéder à un bureau distant via un navigateur.
    - **Avantage** : Pas besoin d'installer un client VNC sur la machine locale.
    - **Fonctionnement** :
        - noVNC utilise **WebSockets** pour transmettre les données entre le serveur VNC et le navigateur.
    - **Cas d'utilisation** :
        - Accès aux serveurs distants via un simple lien web.
        - Utilisation dans les environnements cloud (OpenStack, Proxmox).

---

## **Chapitre 2 : Services d’annuaires LDAP et authentification Kerberos**

#### **LDAP (Lightweight Directory Access Protocol)**

LDAP est un **protocole standardisé** pour accéder à un annuaire centralisé utilisé pour gérer des informations hiérarchiques comme des utilisateurs, des groupes, des appareils ou des services. Voici une vue complète pour tout comprendre, y compris les concepts essentiels comme les `objectClass` :

---

#### **Structure hiérarchique de LDAP**

- **DIT (Directory Information Tree)** :
    - L'annuaire LDAP est organisé comme un **arbre hiérarchique**.
    - Chaque **entrée (entry)** représente un objet (utilisateur, groupe, appareil, etc.).
    - Chaque entrée a un **DN (Distinguished Name)** qui l'identifie de manière unique.

##### **Composants principaux :**

1. **DN (Distinguished Name)** :
    
    - Identifie une entrée dans l’arbre en combinant tous ses composants hiérarchiques.
    - Exemple de DN :
        
        ```
        dn: uid=john,ou=People,dc=example,dc=com
        ```
        
        - **uid=john** : Identifiant unique de l'utilisateur.
        - **ou=People** : Organisation ou sous-arbre où est stocké l'utilisateur.
        - **dc=example,dc=com** : Nom de domaine du serveur LDAP.
2. **RDN (Relative Distinguished Name)** :
    
    - Chaque composant du DN. Exemple : `uid=john`.

---

#### **Principes clés**

1. **ObjectClass** :
    
    - Définit le type d'objet dans l'annuaire et les attributs qui lui sont associés.
    - Chaque entrée LDAP a une ou plusieurs `objectClass`.
    - Les **classes d'objet** définissent :
        - **Attributs obligatoires** : Doivent être présents dans l'entrée.
        - **Attributs optionnels** : Peuvent être ajoutés.
    - Exemple d'`objectClass` pour un utilisateur :
        
        ```ldif
        dn: uid=john,ou=People,dc=example,dc=com
        objectClass: inetOrgPerson
        objectClass: posixAccount
        uid: john
        cn: John Doe
        sn: Doe
        mail: john@example.com
        userPassword: secret
        ```
        
        - **`inetOrgPerson`** : Définit des attributs pour une personne (nom, mail, mot de passe, etc.).
        - **`posixAccount`** : Ajoute des informations pour une gestion Unix/Linux (UID, groupe, etc.).
2. **Attributs courants** :
    
    - **`cn`** : Common Name (nom complet).
    - **`uid`** : Identifiant unique pour l’utilisateur.
    - **`userPassword`** : Mot de passe de l'utilisateur.
    - **`mail`** : Adresse e-mail.
    - **`uidNumber`** : Identifiant numérique Unix pour l’utilisateur.
    - **`gidNumber`** : Groupe associé.
3. **DIT et suffixe LDAP** :
    
    - La racine de l’annuaire est définie par un **suffixe**. Exemple :
        - Suffixe : `dc=example,dc=com`.
        - Représente la base de l’arbre.

---

#### **Exemple complet d’un fichier LDIF (création d’un utilisateur)**

```ldif
dn: uid=john,ou=People,dc=example,dc=com
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: shadowAccount
uid: john
cn: John Doe
sn: Doe
mail: john@example.com
userPassword: {SSHA}hashedpassword
uidNumber: 1001
gidNumber: 1001
homeDirectory: /home/john
```

---

#### **Applications de LDAP**

1. **Authentification centralisée** :
    - Utilisé par les services réseau (SSH, Samba, etc.) pour valider les utilisateurs.
2. **Gestion des comptes Unix/Linux** :
    - Remplace les fichiers `/etc/passwd` et `/etc/shadow`.
3. **Stockage des certificats électroniques** :
    - Gère des données pour des systèmes de sécurité.

---


### **Kerberos**

Kerberos est un protocole d’**authentification sécurisé** basé sur la cryptographie symétrique. Il est conçu pour protéger les services réseau contre les attaques et fournit une méthode d’authentification unique (**Single Sign-On**).

---

#### **Principe de fonctionnement : Les tickets**

- Kerberos utilise un **système de tickets** pour prouver l'identité d'un utilisateur sans transmettre son mot de passe sur le réseau.

---

#### **Composants principaux**

1. **KDC (Key Distribution Center)** :
    
    - Le serveur central qui gère l'authentification.
    - Composé de :
        - **AS (Authentication Server)** : Authentifie les utilisateurs.
        - **TGS (Ticket Granting Server)** : Fournit des tickets pour accéder aux services.
2. **Tickets Kerberos** :
    
    - **Ticket Granting Ticket (TGT)** : Obtenu après l’authentification initiale, utilisé pour demander d’autres tickets.
    - **Ticket de service (Service Ticket)** : Permet d’accéder à un service spécifique.

---

#### **Processus Kerberos en détail**

1. **Authentification initiale (obtenir un TGT)** :
    
    - L'utilisateur fournit son **nom** et son **mot de passe**.
    - Le client envoie une demande au **AS** pour obtenir un TGT.
    - Le AS vérifie les informations et envoie un TGT chiffré avec la clé de session.
2. **Accès à un service (obtenir un ticket de service)** :
    
    - Le client utilise le TGT pour demander un **ticket de service** au TGS.
    - Le TGS génère un ticket de service contenant des informations sur l’utilisateur.
3. **Connexion au service** :
    
    - Le client envoie le **ticket de service** au serveur cible.
    - Le serveur déchiffre le ticket avec sa clé privée pour vérifier l’identité.

---

#### **Exemple d’échanges Kerberos**

1. **Utilisateur Pierre** veut accéder au service `fileserver.example.com`.
2. **Authentification auprès du KDC** :
    - Pierre envoie une demande au AS.
    - Le AS génère un TGT pour Pierre, chiffré avec la clé de Pierre.
3. **Demande de ticket de service** :
    - Pierre utilise son TGT pour demander un ticket pour `fileserver.example.com`.
    - Le TGS génère un ticket pour le service, chiffré avec la clé du serveur.
4. **Accès au service** :
    - Pierre présente son ticket au serveur `fileserver.example.com`.
    - Le serveur valide le ticket et établit une session sécurisée.

---

#### **Avantages de Kerberos**

1. **Single Sign-On (SSO)** :
    - L'utilisateur ne s’authentifie qu’une fois pour accéder à plusieurs services.
2. **Sécurité renforcée** :
    - Les mots de passe ne sont jamais transmis sur le réseau.
    - Les tickets ont une durée de vie limitée, réduisant les risques d’attaques par rejeu.
3. **Interopérabilité** :
    - Fonctionne avec LDAP, Active Directory, SSH, etc.

---



#### **Résumé des étapes pour une configuration Kerberos**

1. Configurer le **KDC** (Key Distribution Center).
2. Créer les **principals** pour les utilisateurs et services.
3. Configurer les clients pour utiliser le KDC.
4. Synchroniser les horloges sur toutes les machines (important pour éviter les erreurs d’horodatage).



### BONUS

[Kerberos vs LDAP](https://www.youtube.com/watch?v=Xjpi8xYqPcY)
  --- 
## **Chapitre 3 : Services PXE et DNS avancé**

#### **Service PXE**

- **PXE (Preboot Execution Environment)** : Permet de démarrer une machine via un réseau sans disque dur local.
- Utilise :
    - **DHCP** : Pour attribuer une adresse IP.
    - **TFTP** : Pour transférer l’image système.

#### **DNS avancé**

- **Fonctionnement DNS** :
    
    - Associe un nom de domaine à une adresse IP.
    - Hiérarchisé en zones (racine, TLD, domaines).
- **Enregistrements avancés** :
    
    - **SRV** : Localise des services spécifiques (SIP, LDAP, Kerberos).
    - **NAPTR** : Supporte des fonctionnalités comme la mobilité des numéros dans les réseaux VoIP.
##### **Introduction aux enregistrements DNS**

Un serveur DNS (Domain Name System) traduit les noms de domaine en adresses IP et fournit des informations supplémentaires sur les services associés à un domaine via des **enregistrements DNS**.

Les enregistrements de base incluent :

- **A** : Associe un nom de domaine à une adresse IPv4.
- **AAAA** : Associe un nom de domaine à une adresse IPv6.
- **CNAME** : Alias pour un autre domaine.
- **MX** : Indique les serveurs de messagerie pour un domaine.

##### **Enregistrements avancés**

1. **SRV (Service Record)**
    
    - Localise des services spécifiques dans un domaine (ex : SIP, LDAP, Kerberos, etc.).
    - Contient des informations telles que :
        - Le service et protocole (ex : `_sip._tcp`).
        - La priorité (pour trier plusieurs services).
        - Le poids (pour équilibrer la charge).
        - Le port utilisé par le service.
        - Le nom d’hôte qui héberge le service.
    
    **Exemple d’enregistrement SRV** :  
    Pour un serveur SIP utilisant TCP :
    
    ```
    _sip._tcp.example.com.  IN SRV  10 60 5060 sipserver.example.com.
    ```
    
    - **`_sip`** : Nom du service (SIP ici).
    - **`_tcp`** : Protocole utilisé (TCP ici).
    - **`10`** : Priorité (plus le nombre est petit, plus la priorité est élevée).
    - **`60`** : Poids pour répartir la charge.
    - **`5060`** : Port utilisé par le service.
    - **`sipserver.example.com`** : Serveur offrant ce service.
2. **NAPTR (Name Authority Pointer)**
    
    - Utilisé pour des applications complexes comme la VoIP (Voice over IP).
    - Fournit des informations sur la résolution des noms (ex : traduire un numéro de téléphone en adresse SIP).
    - Peut être combiné avec SRV pour une recherche hiérarchique.
    
    **Exemple d’enregistrement NAPTR** :
    
    ```
    example.com.  IN  NAPTR 100 10 "U" "E2U+sip" "!^.*$!sip:info@example.com!" .
    ```
    
    - **`100`** : Ordre de priorité.
    - **`10`** : Poids.
    - **`"U"`** : Drapeau indiquant que cet enregistrement est un remplacement.
    - **`"E2U+sip"`** : Service à utiliser (SIP ici).
    - **`"!^.*$!sip:info@example.com!"`** : Remplacement pour la résolution.
3. **PTR (Pointer Record)**
    
    - Utilisé pour la résolution inverse (trouver le nom de domaine associé à une adresse IP).
    - Enregistré dans la zone **in-addr.arpa** pour IPv4 ou **ip6.arpa** pour IPv6.
    
    **Exemple d’enregistrement PTR** :
    
    ```
    10.1.168.192.in-addr.arpa.  IN PTR server.example.com.
    ```
    
4. **TXT (Text Record)**
    
    - Stocke des informations textuelles pour un domaine.
    - Utilisé pour SPF (Sender Policy Framework), DKIM, et d’autres configurations.
    
    **Exemple d’enregistrement TXT** :
    
    ```
    example.com.  IN TXT  "v=spf1 include:_spf.google.com ~all"
    ```
    

---


## **Chapitre 4 : Messagerie classique et instantanée**

#### **Définition de la messagerie**

- **Messagerie classique (e-mail)** : Système d’échange de messages via des serveurs (SMTP, IMAP, POP3).
- **Messagerie instantanée** : Communication en temps réel (WhatsApp, Teams).

#### **Composants fondamentaux**

1. **Client de messagerie (MUA)** : Interface utilisateur (Outlook, Thunderbird).
2. **Serveur de messagerie** :
    - **MTA (Mail Transfer Agent)** : Transfère les e-mails (ex : Postfix).
    - **MDA (Mail Delivery Agent)** : Livre les e-mails dans les boîtes aux lettres.
3. **Protocoles** :
    - **SMTP** : Envoi des messages.
    - **IMAP/POP3** : Récupération des messages.

#### **Formats de boîte aux lettres**

1. **Mailbox** : Un fichier unique par utilisateur contenant tous les messages.
2. **Maildir** : Un dossier par utilisateur, chaque mail est un fichier distinct.

---

---

# Pratique

Très bien, je vais reprendre la **partie pratique de chaque service** de manière détaillée, claire et précise, avec des étapes étape par étape pour faciliter l'apprentissage. Chaque section comportera :

1. Une **introduction pratique** pour comprendre le contexte.
2. Les **étapes de configuration** avec les commandes exactes.
3. Les fichiers de configuration essentiels, leurs explications.
4. Les tests ou vérifications à réaliser pour s'assurer que tout fonctionne.

---

## **Chapitre 1 : Travail en environnement hybride et partage de ressources**

#### **Service Samba : Partage de ressources en environnement hétérogène (Linux et Windows)**

##### **Objectif :**

Configurer un serveur Samba sous Linux pour partager des dossiers accessibles depuis une machine Windows.

##### **Étapes pratiques :**

1. **Installation de Samba :**
    
    ```bash
    sudo apt update
    sudo apt install samba
    ```
    
    - Cette commande installe Samba et ses dépendances.
2. **Création d’un dossier à partager :**
    
    ```bash
    mkdir -p /home/user/partage
    sudo chmod -R 755 /home/user/partage
    ```
    
    - **`mkdir -p`** : Crée le dossier partagé.
    - **`chmod`** : Donne les permissions nécessaires pour que tous les utilisateurs puissent y accéder.
3. **Configuration de Samba :**
    
    - Ouvrir le fichier de configuration Samba :
        
        ```bash
        sudo nano /etc/samba/smb.conf
        ```
        
    - Ajouter la configuration suivante à la fin du fichier :
        
```ini
        [Partage1]
        comment = Dossier partagé pour Windows
        path = /home/user/partage
        browsable = yes
        read only = no
        create mask = 0755
        force user = nobody
        force group = nogroup
```
        
- Explications des options :
        - **`comment`** : Description visible du dossier partagé.
        - **`path`** : Chemin du dossier à partager.
        - **`read only`** : Détermine si le dossier est en lecture seule.
        - **`force user/group`** : Définit les permissions utilisateur/groupe par défaut.
    
1. **Création d’un utilisateur Samba :**
    
    - Ajouter un utilisateur système si nécessaire :
        
        ```bash
        sudo adduser toto
        ```
        
    - Ajouter cet utilisateur à Samba :
        
        ```bash
        sudo smbpasswd -a toto
        ```
        
        - Cette commande crée un mot de passe Samba pour l'utilisateur.
5. **Redémarrage du service Samba :**
    
    ```bash
    sudo systemctl restart smbd
    sudo systemctl enable smbd
    ```
    
6. **Tester la configuration :**
    
    - Vérifier que le fichier Samba est valide :
        
        ```bash
        testparm
        ```
        
    - Accéder au dossier partagé depuis une machine Windows :
        - Ouvrir l’explorateur Windows.
        - Taper `\\<IP_du_serveur>` dans la barre d'adresse.
        - Vous devriez voir le dossier **Partage1**.
#### **1. Pratique : Configuration de VNC et noVNC**

##### **Étapes pour VNC : Configuration sous Linux (exemple avec TigerVNC)**

1. **Installer TigerVNC :**
    
    ```bash
    sudo apt update
    sudo apt install tigervnc-standalone-server tigervnc-common
    ```
    
2. **Configurer le serveur VNC :**
    
    - Démarrer un bureau graphique pour un utilisateur :
        
        ```bash
        vncserver :1
        ```
        
        - Le `:1` représente un écran virtuel. L’adresse complète sera `localhost:5901` (port 5900 + 1).
        - Un mot de passe vous sera demandé pour sécuriser la session.
3. **Configurer les paramètres graphiques :**
    
    - Arrêter le serveur pour configurer les fichiers :
        
        ```bash
        vncserver -kill :1
        ```
        
    - Modifier le fichier de configuration utilisateur (`~/.vnc/xstartup`) :
        
        ```bash
        nano ~/.vnc/xstartup
        ```
        
        - Exemple pour XFCE :
            
            ```bash
            #!/bin/bash
            xrdb $HOME/.Xresources
            startxfce4 &
            ```
            
    - Rendre le fichier exécutable :
        
        ```bash
        chmod +x ~/.vnc/xstartup
        ```
        
4. **Redémarrer le serveur VNC :**
    
    ```bash
    vncserver :1
    ```
    
5. **Se connecter depuis un client VNC :**
    
    - Téléchargez un client comme **RealVNC** ou **TightVNC Viewer**.
    - Connectez-vous avec : `IP_serveur:5901`.

---

##### **Étapes pour noVNC : Accès VNC via navigateur**

1. **Installer noVNC et WebSockify :**
    
    ```bash
    sudo apt install novnc websockify
    ```
    
2. **Lancer noVNC avec le serveur VNC :**
    
    - Identifiez le port du serveur VNC (ex : 5901).
    - Démarrez noVNC avec WebSockify :
        
        ```bash
        websockify --web=/usr/share/novnc 6080 localhost:5901
        ```
        
        - **6080** : Port utilisé pour accéder à noVNC.
        - **localhost:5901** : Adresse du serveur VNC.
3. **Accéder à noVNC via le navigateur :**
    
    - Ouvrez votre navigateur et entrez l'URL :
        
        ```
        http://<IP_serveur>:6080/vnc.html
        ```
        
    - Entrez le mot de passe VNC pour accéder au bureau distant.
4. **Configurer noVNC en service permanent (optionnel) :**
    
    - Créez un service systemd pour lancer noVNC automatiquement au démarrage :
        
        ```bash
        sudo nano /etc/systemd/system/novnc.service
        ```
        
        - Exemple de contenu :
            
            ```conf
            [Unit]
            Description=noVNC server
            After=network.target
            
            [Service]
            ExecStart=/usr/bin/websockify --web=/usr/share/novnc 6080 localhost:5901
            Restart=always
            User=your_user
            
            [Install]
            WantedBy=multi-user.target
            ```
            
    - Activez le service :
        
        ```bash
        sudo systemctl enable novnc
        sudo systemctl start novnc
        ```
        

---

#### **2. Tests et Vérifications**

- **Pour VNC** :
    
    - Utilisez un client VNC pour vous connecter : `IP_serveur:5901`.
    - Vérifiez que l'interface graphique s'affiche correctement.
- **Pour noVNC** :
    
    - Testez l'accès via le navigateur : `http://<IP_serveur>:6080/vnc.html`.
    - Assurez-vous que l'accès est sécurisé avec un mot de passe.

---

---

## **Chapitre 2 : LDAP et Kerberos**

#### **Service LDAP**

##### **Objectif :**

Configurer OpenLDAP pour gérer les utilisateurs.

##### **Étapes pratiques :**

1. **Installer LDAP :**
    
    ```bash
    sudo apt install slapd ldap-utils
    sudo dpkg-reconfigure slapd
    ```
    
2. **Ajouter des utilisateurs via LDIF :**
    
    - Exemple de fichier `user.ldif` :
        
        ```ldif
        dn: uid=john,ou=People,dc=example,dc=com
        objectClass: inetOrgPerson
        uid: john
        sn: Doe
        cn: John Doe
        mail: john@example.com
        userPassword: secret
        ```
        
    - Ajouter l’utilisateur :
        
        ```bash
        ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f user.ldif
        ```
        

---


## **Chapitre 3 : Services PXE et DNS**

#### **Service PXE**

##### **Objectif :**

Configurer un serveur PXE pour installer un système d’exploitation sur un client via le réseau.

##### **Étapes pratiques :**

1. **Installer les paquets nécessaires :**
    
    ```bash
    sudo apt install isc-dhcp-server tftpd-hpa syslinux
    ```
    
2. **Configurer le serveur DHCP :**
    
    - Modifier `/etc/dhcp/dhcpd.conf` :
        
        ```conf
        subnet 192.168.1.0 netmask 255.255.255.0 {
          range 192.168.1.100 192.168.1.200;
          option routers 192.168.1.1;
          filename "pxelinux.0";
          next-server 192.168.1.10;
        }
        ```
        
        - **`filename`** : Nom du fichier de démarrage pour PXE.
        - **`next-server`** : Adresse IP du serveur TFTP.
3. **Configurer TFTP :**
    
    - Modifier `/etc/default/tftpd-hpa` :
        
        ```conf
        TFTP_DIRECTORY="/var/lib/tftpboot"
        RUN_DAEMON="yes"
        OPTIONS="-l -s /var/lib/tftpboot"
        ```
        
4. **Ajouter des fichiers de démarrage :**
    
    - Copier le fichier `pxelinux.0` :
        
        ```bash
        cp /usr/lib/PXELINUX/pxelinux.0 /var/lib/tftpboot
        ```
        
    - Créer le dossier pour les images système :
        
        ```bash
        mkdir -p /var/lib/tftpboot/pxelinux.cfg
        ```
        
5. **Redémarrer les services :**
    
    ```bash
    sudo systemctl restart isc-dhcp-server tftpd-hpa
    ```
    
6. **Tester le service PXE :**
    
    - Configurer un client avec une option de démarrage PXE dans le BIOS.
    - Redémarrer le client pour vérifier que l’installation démarre via le réseau.

---

#### **Service DNS avec enregistrements avancés**

##### **Objectif :**

Configurer un serveur DNS avec des enregistrements SRV et NAPTR.

##### **Étapes pratiques :**

1. **Installer le serveur DNS BIND :**
    
    ```bash
    sudo apt install bind9
    ```
    

2. Modifier le fichier `/etc/bind/named.conf.local` pour ajouter une nouvelle zone :
    
    ```conf
    zone "example.com" {
        type master;
        file "/etc/bind/db.example.com";
    };
    ```
    
3. Créer le fichier de zone `/etc/bind/db.example.com` :
    
    ```conf
    $TTL 86400
    @   IN  SOA  ns.example.com. admin.example.com. (
            2025012701 ; Serial
            3600       ; Refresh
            1800       ; Retry
            1209600    ; Expire
            86400      ; Minimum TTL
        )
    @   IN  NS    ns.example.com.
    ns  IN  A     192.168.1.10
    www IN  A     192.168.1.20
    _sip._tcp IN  SRV 10 60 5060 sipserver.example.com.
    example.com. IN  NAPTR 100 10 "U" "E2U+sip" "!^.*$!sip:info@example.com!" .
    ```
    
4. Redémarrer le serveur DNS BIND :
    
    ```bash
    sudo systemctl restart bind9
    ```
    
5. Tester les enregistrements DNS :
    
    - Pour SRV :
        
        ```bash
        dig @192.168.1.10 example.com SRV
        ```
        
    - Pour NAPTR :
        
        ```bash
        dig @192.168.1.10 example.com NAPTR
        ```
        



---


## **Chapitre 4 : Services de messagerie**

#### **4.1 SMTP avec Postfix**

##### **Objectif :**

Configurer un serveur SMTP (Simple Mail Transfer Protocol) avec Postfix pour l'envoi de courriels.

---

##### **Étapes pratiques pour Postfix :**

1. **Installer Postfix :**
    - Mettre à jour les paquets et installer Postfix :
        
        ```bash
        sudo apt update
        sudo apt install postfix
        ```
        
    - Pendant l’installation, choisissez le type de configuration **"Site Internet"** :
        - **Nom de courrier du système** : Exemple : `mail.example.com`.

---

2. **Configurer Postfix :**
    - Ouvrir le fichier `/etc/postfix/main.cf` pour modifier les paramètres principaux :
        
        ```bash
        sudo nano /etc/postfix/main.cf
        ```
        
    - Ajouter ou modifier les lignes suivantes :
        
        ```conf
        myhostname = mail.example.com      # Nom de l'hôte de votre serveur
        mydomain = example.com             # Nom de domaine principal
        myorigin = $mydomain               # Adresse expéditeur des e-mails
        inet_interfaces = all              # Ecouter sur toutes les interfaces
        mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
        relayhost =                        # Laisser vide si aucun relai externe n'est utilisé
        home_mailbox = Maildir/            # Format de boîte aux lettres (Maildir)
        ```
        
        **Explications des paramètres principaux :**
        - **`myhostname`** : Nom du serveur (FQDN).
        - **`myorigin`** : Définit le domaine utilisé pour les expéditeurs.
        - **`inet_interfaces`** : Spécifie les interfaces sur lesquelles Postfix écoute.
        - **`home_mailbox`** : Utilisation du format **Maildir**, qui stocke chaque e-mail dans un fichier distinct.

---

3. **Créer un utilisateur pour tester :**
    - Ajouter un utilisateur pour tester la messagerie :
        
        ```bash
        sudo adduser testuser
        ```
        
    - Configurer les permissions pour son répertoire Maildir :
        
        ```bash
        sudo chmod -R 700 /home/testuser/Maildir
        ```
        

---

4. **Tester Postfix :**
    - Redémarrer Postfix :
        
        ```bash
        sudo systemctl restart postfix
        ```
        
    - Envoyer un e-mail en ligne de commande :
        
        ```bash
        echo "Ceci est un test" | mail -s "Test de Postfix" testuser@example.com
        ```
        
    - Vérifier la réception dans le fichier `/var/log/mail.log`.

---

#### **4.2 IMAP avec Dovecot**

##### **Objectif :**

Configurer Dovecot pour permettre aux utilisateurs de récupérer leurs courriels via les protocoles IMAP et POP3.

---

##### **Étapes pratiques pour Dovecot :**

1. **Installer Dovecot :**
    - Installer les paquets nécessaires :
        
        ```bash
        sudo apt install dovecot-imapd dovecot-pop3d
        ```
        

---

2. **Configurer Dovecot :**
    - Modifier le fichier `/etc/dovecot/dovecot.conf` :
        
        ```bash
        sudo nano /etc/dovecot/dovecot.conf
        ```
        
    - Vérifier que les lignes suivantes sont présentes et correctement configurées :
        
        ```conf
        mail_location = maildir:~/Maildir      # Format des boîtes aux lettres
        protocols = imap pop3                 # Activer IMAP et POP3
        ```
        
    - **Configurer l’authentification :**
        - Vérifier le fichier `/etc/dovecot/conf.d/10-auth.conf` :
            
            ```conf
            disable_plaintext_auth = no
            auth_mechanisms = plain login
            ```
            
    - **Configurer le service IMAP :**
        - Modifier le fichier `/etc/dovecot/conf.d/10-master.conf` :
            
            ```conf
            service imap-login {
                inet_listener imap {
                    port = 143
                }
            }
            ```
            

---

3. **Tester Dovecot :**
    - Redémarrer Dovecot :
        
        ```bash
        sudo systemctl restart dovecot
        ```
        
    - Tester l’accès IMAP depuis un client de messagerie comme Thunderbird ou en ligne de commande :
        
        ```bash
        telnet localhost 143
        ```
        

---

#### **4.3 Tests complets du serveur de messagerie**

1. **Envoyer un e-mail avec Postfix :**
    
    - Utiliser la commande suivante pour envoyer un e-mail à un utilisateur local :
        
        ```bash
        echo "Message de test SMTP" | mail -s "Test SMTP" testuser@example.com
        ```
        
2. **Vérifier la réception avec Dovecot :**
    
    - Connecter un client IMAP (comme Thunderbird) :
        - Serveur entrant : `mail.example.com` (IMAP, port 143).
        - Serveur sortant : `mail.example.com` (SMTP, port 25).
3. **Analyser les logs :**
    
    - **Postfix** :
        
        ```bash
        sudo tail -f /var/log/mail.log
        ```
        
    - **Dovecot** :
        
        ```bash
        sudo tail -f /var/log/dovecot.log
        ```
        

---

#### **Résumé des fichiers modifiés**

1. **Postfix : `/etc/postfix/main.cf`**
    - Définit les paramètres SMTP.
2. **Dovecot : `/etc/dovecot/dovecot.conf`**
    - Configure IMAP, POP3, et le format des boîtes aux lettres.

---

### **Résumé des rôles dans un système de messagerie :**

|**Composant**|**Rôle**|**Exemples courants**|
|---|---|---|
|**MUA** (Mail User Agent)|Application utilisée par l'utilisateur pour gérer ses e-mails|Thunderbird, Outlook, Gmail|
|**MTA** (Mail Transfer Agent)|Transfert d'e-mails entre serveurs|Postfix, Exim, Sendmail|
|**MDA** (Mail Delivery Agent)|Livraison des e-mails dans la boîte locale|Procmail, Dovecot LDA|
|**IMAP/POP3 Server**|Fournit l'accès aux e-mails stockés|Dovecot, Courier|

---



# Sigle

##  SSH (Secure Shell) : 22
## RDP (Remote Desktop Protocol) : 3389

## PAP (Password Authentication Protocol)

## CHAP (Challenge Handshake  Authentication Protocol)

## MSCHAP (Microsoft Challenge Handshake  Authentication Protocol)

## RADIUS (Remote Authentication Dial-in User Service) : 1812

## LDAP (Lightweight Directory Access Protocol) : 389

## LDIF (LDAP Data Interchange Format )

## DIT (Directory Information Tree)

## DN ( Distinguish Name)

## DSE (Directory Service Entry)
## RDN (Relative Distinguish Name)

## DC  (DomainComponent)

## DUA (Directory User Agent)

## DSA (Directory Service Agent)

## DIB ( Directory Information Base)

## MUA (Mail User Agent)

## MTA ( Mail Transfert Agent)

## MDA ( Mail deliver Agent)

## SMTP ( Simple Mail Transfert Protocol) : 25

## POP (Post Office Protocol) : 110 et 995

## IMAP (Internet Mail  Access Protocol) : 143 et 993











# Système d'apprentissage


### **Chapitre 1 : Travail environnement hybride et partage de ressources**

<font color="#de7802">Première session : 25 minutes de théorie</font>


<font color="#00b050">Pause de 5 minutes</font>

- **Rappelle-toi de l'importance** : Tu vas comprendre comment gérer des environnements hybrides. C’est essentiel dans le monde du travail moderne ! Rappelle-toi que chaque notion maîtrisée te rapproche d’une meilleure gestion des ressources en entreprise.
- **Conseil pour la pause** :
    - **Célèbre ta compréhension** : Même si c’est un début, félicite-toi pour chaque détail que tu as saisi. Ces petites victoires sont importantes.
    - **Respiration ou étirements** : Fais une courte séance de respiration pour libérer l'esprit et recharger ton énergie pour la pratique.

<font color="#de7802">Deuxième session : 25 minutes de pratique</font>


<font color="#00b050">Pause de 5 minutes</font>

- **Mise en application** : C’est le moment de tester ce que tu viens d’apprendre. Configurer un environnement hybride ou tester des outils de partage de ressources va renforcer ta compréhension.
- **Conseil pour la pause** :
    - **Récompense-toi** : Prends un petit en-cas ou une boisson pour te féliciter du travail accompli.
    - **Légère activité physique** : Fais une petite marche ou des étirements pour détendre tes muscles et recharger ton énergie physique.

---

### **Chapitre 2 : Services PXE et DNS avancés**

<font color="#de7802">Première session : 25 minutes de théorie</font>

- **Renforce ton savoir-faire technique** : Apprendre le PXE et les DNS avancés t’amène à une expertise technique précieuse. Tu vas comprendre les bases d’un réseau, et cela te donnera de nouvelles compétences.
- **Conseil pour la pause** :
    - **Rappelle-toi de ton objectif** : Tu es en train d’acquérir une expertise que peu de gens maîtrisent, et cela peut t'ouvrir beaucoup de portes professionnelles.
    - **Détente rapide** : Écoute un peu de musique ou fais quelques respirations profondes pour garder une tête claire.

<font color="#00b050">Pause de 5 minutes</font>

<font color="#de7802">Deuxième session : 25 minutes de pratique</font>

- **Teste tes connaissances** : En pratiquant la configuration de PXE ou l’installation d’un serveur DNS, tu fais un bond dans ta compréhension pratique de ces concepts.
- **Conseil pour la pause** :
    - **Prends une récompense** : Une pause café ou un snack peut t'aider à apprécier ton progrès.
    - **Détente physique** : Fais quelques étirements ou marche un peu pour activer ton corps avant de redémarrer.

<font color="#00b050">Pause de 5 minutes</font>

---

### **Chapitre 3 : Service d’annuaires LDAP et authentification Kerberos**

<font color="#de7802">Première session : 25 minutes de théorie</font>

- **Consolide tes connaissances sur la sécurité** : LDAP et Kerberos sont essentiels pour la gestion des identités et des accès dans un réseau. Maîtriser ces services te place dans une position stratégique en termes de sécurité informatique.
- **Conseil pour la pause** :
    - **Prends un moment pour respirer** : Réfléchis à ce que tu viens d'apprendre et à son importance dans la sécurité des réseaux.
    - **Renforce ta motivation** : Tu es en train d'acquérir des compétences qui sont recherchées dans de nombreux secteurs technologiques.

<font color="#00b050">Pause de 5 minutes</font>

<font color="#de7802">Deuxième session : 25 minutes de pratique</font>

- **Application concrète** : La mise en place d’un annuaire LDAP ou la configuration de l’authentification Kerberos te permettra de bien comprendre comment ces services interagissent.
- **Conseil pour la pause** :
    - **Récompense-toi** : Après avoir configuré un système, prends une petite pause pour marquer ta progression.
    - **Détente physique** : Fais des étirements ou prends l'air pour recharger tes batteries avant de revenir à la tâche.

<font color="#00b050">Pause de 5 minutes</font>

---

### **Chapitre 4 : Messagerie classique et instantanée**

<font color="#de7802">Première session : 25 minutes de théorie</font>

- **Compréhension des systèmes de messagerie** : Tu vas apprendre les différences entre les systèmes de messagerie classique et instantanée. Ces compétences sont utiles dans de nombreuses entreprises modernes.
- **Conseil pour la pause** :
    - **Visualise ton succès** : Imagine-toi en train de configurer et de gérer des systèmes de messagerie complexes dans un environnement professionnel.
    - **Détente rapide** : Fais une respiration profonde ou une pause visuelle pour recharger ton esprit.

<font color="#00b050">Pause de 5 minutes</font>

<font color="#de7802">Deuxième session : 25 minutes de théorie</font>

- **Approfondis ta compréhension** : En étudiant plus en profondeur les protocoles de messagerie, tu vas pouvoir mieux comprendre leur fonctionnement et résoudre des problèmes techniques en cas de besoin.
- **Conseil pour la pause** :
    - **Rappelle-toi pourquoi tu apprends cela** : Ces connaissances ouvrent des portes dans l’administration réseau, la gestion de serveurs de messagerie, et la communication sécurisée.
    - **Activité légère** : Fais une courte activité physique pour rester concentré et revigoré.

<font color="#00b050">Pause de 20 minutes</font>

- **Change d’environnement** : Profite de cette pause plus longue pour sortir, respirer profondément, et faire le plein d’énergie. C’est un moment idéal pour te déconnecter et revenir avec un esprit frais pour le dernier chapitre ou révision.

---


_"Le succès ne vient pas de ce que tu fais occasionnellement, mais de ce que tu fais constamment."_ — `Marie Forleo`


![[Pasted image 20250127142951.png|800]]