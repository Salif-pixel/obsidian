  
---

## Pourquoi utiliser Kerberos avec SSH ?

### Authentification centralisée :

En intégrant Kerberos avec SSH, les utilisateurs peuvent s'authentifier une seule fois à l'aide du protocole Kerberos (Single Sign-On, SSO). Une fois authentifiés, ils peuvent accéder à plusieurs serveurs SSH sans devoir entrer leurs mots de passe à chaque fois.

### Sécurité renforcée :

Avec Kerberos, les mots de passe ne sont jamais envoyés sur le réseau, même en cas d’authentification via SSH. Cela réduit les risques d’attaques par interception.

### Gestion simplifiée :

Dans un environnement où de nombreux serveurs SSH doivent être gérés, Kerberos offre une solution centralisée pour gérer les identifiants des utilisateurs et leurs permissions.

### Délégation des identifiants :

Kerberos permet également la délégation d’identifiants (via GSSAPI), ce qui signifie qu’un utilisateur peut transmettre ses droits d’accès Kerberos à un autre service ou système de manière sécurisée.

## Fonctionnement général

L’intégration de Kerberos avec SSH repose sur le protocole GSSAPI (Generic Security Services API), qui permet à SSH d’utiliser les tickets Kerberos pour authentifier les utilisateurs. Lorsque vous vous connectez via SSH à un serveur Kerberos-enabled, voici ce qui se passe :

1. Le client obtient un ticket d’authentification auprès du serveur Kerberos (via l’utilitaire `kinit`).
2. Ce ticket est utilisé pour authentifier le client auprès du serveur SSH sans qu’il soit nécessaire d’entrer un mot de passe.
3. Une fois l’authentification réussie, une session chiffrée SSH est établie.

---

## Configurer SSH pour utiliser Kerberos

### Côté serveur :

1. **Créer un principal pour le service SSH** Sur le KDC, créez un principal pour le service SSH :
    
    ```bash
    kadmin.local
    addprinc -randkey SSH/server.dic.sn
    ktadd SSH/server.dic.sn
    ```
    
2. **Configurer le fichier `sshd_config`** Modifiez le fichier `/etc/ssh/sshd_config` pour inclure les options suivantes :
    
    ```bash
    kerberosAuthentication yes
    kerberosOrLocalPasswd yes
    kerberosTicketCleanup yes
    kerberosGetAFSToken no
    ```
    
3. **Redémarrer le service SSH**
    
    ```bash
    sudo systemctl restart ssh
    ```
    

### Côté client :

1. **Installation de `krb5-user`**
    
    ```bash
    sudo apt install krb5-user
    ```
    
    Cet outil est essentiel pour configurer et utiliser un client Kerberos. Il permet d’obtenir des tickets et de s’authentifier sans avoir à entrer de mots de passe pour chaque service.
    
2. **Obtenir un ticket avec `kinit`**
    
    ```bash
    kinit SSH/server@DIC.SN
    ```
    
3. **Vérifier si le ticket est valide**
    
```bash
    klist
    Default principal: SSH/server@DIC.SN
Valid starting       Expires              Service principal
03.01.2025 00:55:10  04.01.2025 00:55:10  krbtgt/DIC.SN@DIC.SN
root@server:/etc/freeradius/3.0/mods-enabled# 

```
    
4. **Tester la connexion SSH**
    
    ```bash
    ssh -K server.dic.sn
    ```
    
    Cette commande teste l’authentification Kerberos sur SSH. L’option `-K` force l’utilisation de Kerberos.
    

---

Avec cette configuration, vous pouvez vous connecter au serveur SSH sans avoir besoin de saisir un mot de passe, grâce à l’authentification centralisée de Kerberos.