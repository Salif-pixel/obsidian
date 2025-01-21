

---
## Objectif

Configurer un serveur NFS sécurisé avec Kerberos pour garantir que seuls les utilisateurs authentifiés via Kerberos peuvent accéder aux partages NFS.

---

## Prérequis

1. Un serveur Kerberos (KDC) fonctionnel avec un domaine Kerberos (exemple : `DIC.SN`).
2. Deux machines :
    - Une pour le **serveur NFS**.
    - Une pour le **client NFS**.
3. Paquets nécessaires installés sur les deux machines.

---

## Étape 1 : Installer les paquets nécessaires

### Sur le serveur NFS

```bash
sudo apt update
sudo apt install nfs-kernel-server krb5-user
```

### Sur le client NFS

```bash
sudo apt update
sudo apt install nfs-common krb5-user
```

---

## Étape 2 : Configurer Kerberos pour NFS

### Créer un principal pour le service NFS

Sur le KDC :

```bash
kadmin.local
addprinc -randkey NFS/server.dic.sn
ktadd -k /etc/krb5.keytab NFS/server.dic.sn
```

### Copier le fichier keytab

Assurez-vous que le fichier `/etc/krb5.keytab` est disponible sur le serveur NFS :

```bash
sudo chmod 600 /etc/krb5.keytab
```

---

## Étape 3 : Configurer le serveur NFS

1. **Éditer le fichier `/etc/exports`** : Ajoutez une ligne pour partager un répertoire avec une sécurité Kerberos :
    
    ```text
    /srv/nfs_share client.dic.sn(rw,sec=krb5)
    ```
    
    - `sec=krb5` : Permet uniquement les connexions authentifiées via Kerberos.
    - `rw` : Donne un accès en lecture et écriture.
2. **Créer le répertoire à partager** :
    
    ```bash
    sudo mkdir -p /srv/nfs_share
    sudo chown nobody:nogroup /srv/nfs_share
    sudo chmod 755 /srv/nfs_share
    ```
    
3. **Redémarrer le service NFS** :
    
    ```bash
    sudo systemctl restart nfs-kernel-server
    ```
    

---

## Étape 4 : Configurer le client NFS

1. **Obtenir un ticket Kerberos** : Sur le client NFS :
    
    ```bash
    kinit FTP/server@DIC.SN
    ```
    
2. **Monter le partage NFS** : Créez un point de montage et montez le partage avec Kerberos :
    
    ```bash
    sudo mkdir -p /mnt/nfs_share
    sudo mount -t nfs4 -o sec=krb5 server.dic.sn:/srv/nfs_share /mnt/nfs_share
    ```
    
3. **Tester l'accès** : Vérifiez que le client peut accéder au contenu du partage :
    
    ```bash
    ls /mnt/nfs_share
    ```
    

---

## Étape 5 : Vérifications et Dépannage

- **Vérifier les tickets Kerberos** :
    
    ```bash
    klist
    ```
    
- **Logs du serveur NFS** : Consultez les journaux pour identifier les problèmes :
    
    ```bash
    sudo journalctl -u nfs-server
    ```
    
- **Tester le montage automatique** : Ajoutez l'entrée suivante dans `/etc/fstab` pour monter automatiquement le partage :
    
    ```text
    server.dic.sn:/srv/nfs_share /mnt/nfs_share nfs4 sec=krb5 0 0
    ```
    

---

## Conclusion

Avec ces étapes, vous avez configuré un partage NFS sécurisé avec Kerberos. Cela garantit que seuls les utilisateurs authentifiés peuvent accéder au partage, ajoutant ainsi une couche de sécurité supplémentaire à votre environnement réseau. 😊