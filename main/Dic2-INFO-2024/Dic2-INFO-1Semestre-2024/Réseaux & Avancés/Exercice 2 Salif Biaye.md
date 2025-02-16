
---
# Sécurité et Contrôle d’accès

---

## 1. Au niveau du réseau DGI, a-t-on besoin d’un service de contrôle d’accès ?  

>[! Réponse ] 
>Oui

Cela garantit que :  
- Chaque utilisateur (étudiant ou personnel) accède uniquement aux ressources qui lui sont destinées.  
- Les étudiants :  
  - **Ne peuvent pas** modifier leurs notes sur le PGI.  
  - **Peuvent** consulter leurs notes et faire des réclamations.
  - **N'auront** accès qu'au réseau Etudiant et non au Personnel

---

## 2. Est-il pris en charge ? Comment ?  

>[! Réponse ] 
>Oui, cela est géré par des certificats numériques. 
Ces certificats permettent de contrôler l’accès aux ressources.  

### Mécanismes pour le réseau du DGI :
1. **Redirection via pfSense en cas de non-conformité des données :** 
	- Lorsque les informations fournies (par exemple, les identifiants ou données réseau) ne sont pas conformes, l’utilisateur est automatiquement redirigé vers **pfSense**.
	- Cela permet de vérifier et corriger les éventuels problèmes avant d’autoriser l’accès au réseau. 
1. **Certificats numériques exemple X.509 :**
	- Ces certificats garantissent une communication sécurisée et authentifient les équipements ou serveurs du réseau DGI.
2. **Authentification avec identifiants :** 
	- Les utilisateurs se connectent au réseau en utilisant leur **login** et **mot de passe**, associés à des rôles spécifiques.
###  Mécanismes pour le PGI 
  1. **Certificats SSL/TLS :** 
	  - Le certificat du site **etudiant-pgi.esp.sn** est un certificat délivré par **ISRG Root X1**, utilisant l’algorithme de signature **ECDSA avec SHA-384**. Il garantit l’identité du site et sécurise les échanges via HTTPS.
	![[Capture d’écran 2025-01-23 à 23.05.56.png|500]]

  1. **Authentification avec rôles définis :** 
	  - Chaque utilisateur accède au PGI avec son **login** et **mot de passe**, 
	  - et un rôle prédéfini limite ses actions. 
  2. **Jetons d'accès (Tokens) :** 
	  - Lorsqu’un utilisateur se connecte, un jeton temporaire est généré pour valider sa session. 
	  - Cela ajoute une couche de sécurité supplémentaire et limite les risques de réutilisation des identifiants.

---

## 3. Jugez-vous le mécanisme utilisé efficace ?  

>[! Réponse ] 
> Oui

Oui, le mécanisme actuel est efficace, car il assure une gestion rigoureuse des accès et une sécurisation optimale des données sensibles. Voici les raisons pour lesquelles il est efficace :

- **Contrôle d'accès  :** Les utilisateurs sont authentifiés via des identifiants uniques et des certificats numériques, garantissant que seuls les utilisateurs autorisés peuvent accéder aux ressources. Cela permet une gestion précise des permissions et empêche tout accès non autorisé.

- **Sécurisation du réseau :** Le mécanisme de redirection via pfSense assure un contrôle supplémentaire avant d'autoriser l'accès au réseau, et les certificats numériques garantissent une communication sécurisée. Le rôle de pfSense dans la détection des anomalies et dans la gestion des accès contribue à prévenir les risques de sécurité.

- **Protection des données échangées :** Les certificats SSL/TLS garantissent un chiffrement des données sensibles échangées sur le PGI, ce qui protège contre les interceptions malveillantes.

- **Authentification et tokens :** L'utilisation de jetons d'accès ajoute une couche de sécurité en assurant que l'accès à une session est validé de manière temporaire, ce qui empêche une réutilisation frauduleuse des identifiants.

---

## 4. Proposez une solution plus efficace.

**Pour renforcer la sécurité :**

### Réseau DGI :
1. **Surveillance et journalisation :**
    
    - Mettre en place un système de logs pour suivre qui accède au réseau et identifier rapidement les anomalies.
2. **Renforcement des règles via pfSense :**
    
    - Mettre en place des politiques de sécurité supplémentaires avec pfSense pour analyser et contrôler en temps réel le trafic réseau. Cela permettrait de détecter les connexions ou comportements suspects (par exemple, un trafic inhabituel provenant d'un endroit non autorisé) et de les bloquer ou de les restreindre automatiquement. Cette approche garantit que seules les connexions sûres et vérifiées sont autorisées à accéder au réseau, empêchant ainsi les attaques ou les accès non autorisés.
3. **Audits réguliers :**
    
    - Effectuer des audits de sécurité périodiques pour identifier et corriger les vulnérabilités.

4. **Pare-feux de nouvelle génération :** 
	- Utiliser des pare-feux capables d'inspecter en profondeur le trafic réseau pour détecter et bloquer les menaces avancées.
        
### - PGI :
1. **Gestion automatique des certificats :**
    
    - Automatiser le renouvellement et la gestion des certificats SSL/TLS pour garantir une disponibilité continue et éviter les erreurs liées à des certificats expirés.
2. **Formation des utilisateurs :**

    - Renforcer la formation des utilisateurs sur les bonnes pratiques de sécurité pour prévenir les erreurs humaines.
3. **Authentification à plusieurs facteurs :**

    - Ajouter un second facteur (par exemple, une application mobile comme Google Authenticator) pour sécuriser davantage les accès.



---
