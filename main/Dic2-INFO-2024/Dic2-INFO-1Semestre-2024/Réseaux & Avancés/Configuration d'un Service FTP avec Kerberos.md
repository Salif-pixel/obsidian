

Ce document décrit les étapes pour configurer un service FTP authentifié via Kerberos, en utilisant un domaine Kerberos `DIC.SN` et un serveur nommé `server.dic.sn`.

---

## Prérequis

1. Un serveur Kerberos (KDC) configuré et fonctionnel.
2. Un serveur FTP et un client Kerberos compatibles.
3. Domaine Kerberos configuré : `DIC.SN`.
4. Accès root ou sudo sur les machines concernées.

---

## Étape 1 : Installer Kerberos

Sur le serveur FTP et les clients :

```bash
sudo apt update
sudo apt install krb5-user libpam-krb5 vsftpd
```


Configurez `/etc/vsftpd.conf` pour activer PAM :

```ini
pam_service_name=vsftpd
```

---

## Étape 3 : Configurer Kerberos pour le Service FTP
### Configurer PAM pour Kerberos

Créez ou modifiez le fichier `/etc/pam.d/vsftpd` :

```text
auth required pam_krb5.so
account required pam_krb5.so
session required pam_krb5.so
```

---

### Créer un principal pour le service FTP

Sur le serveur KDC :

```bash
kadmin.local
addprinc -randkey FTP/server.dic.sn
ktadd FTP/server.dic.sn
```

Cela crée un principal pour le serveur FTP et ajoute sa clé au fichier `keytab`.

### Copier le fichier keytab

Copiez le fichier `keytab` vers le serveur FTP :

```bash
sudo cp /etc/krb5.keytab /etc/vsftpd.keytab
sudo chmod 600 /etc/vsftpd.keytab
```


## Étape 4 : Tester le Service FTP

### Obtenir un ticket Kerberos

Sur un client configuré pour Kerberos :

```bash
kinit HTTP/server@DIC.SN
```

### Accéder au serveur FTP

Utilisez un client FTP compatible Kerberos, comme `lftp` :

```bash
lftp ftp://server.dic.sn
lftp server.dic.sn:~> 
```

---

## Changement de Mot de Passe d'un Principal

### Modifier le mot de passe

Sur le KDC, utilisez `kadmin.local` :

```bash
kadmin.local
change_password FTP/server.dic.sn
```

### Recréer une clé aléatoire (optionnel)

Pour utiliser un fichier keytab au lieu d'un mot de passe :

```bash
kadmin.local
delprinc FTP/server@DIC.SN
addprinc -randkey FTP/server@DIC.SN
ktadd FTP/server.dic.sn
```

---

## Dépannage

1. **Vérification des journaux :**
    
    - Kerberos : `/var/log/krb5kdc.log`
    - FTP : `/var/log/vsftpd.log`
2. **Vérifier le fichier keytab :**
    
    ```bash
    klist -k
    ```
    
3. **Tester avec un keytab :**
    
    ```bash
    kinit -k -t /etc/vsftpd.keytab FTP/server.dic.sn
    ```
    

---

Avec ces étapes, le service FTP est maintenant configuré pour utiliser Kerberos pour l'authentification. 