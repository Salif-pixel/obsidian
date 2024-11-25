
---

### Critères IPv4 et IPv6

| Critères                      | IPv4                                                  | IPv6                                                                               |
| ----------------------------- | ----------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Plage d'adressage             | 32 bits = 2^32                                        | 128 bits = 2^128                                                                   |
| Type de communications        | Unicast, Multicast, Broadcast                         | Unicast, Multicast, Anycast                                                        |
| Notation                      | Décimale pointée                                      | Hexadécimale avec double point (:)                                                 |
| Organisation                  | Classes                                               | Agrégation                                                                         |
| Nombre d’identifiants Unicast | Variable selon la classe et le nombre de sous-réseaux | Minimum 2^64-1 ou ≥ 2^64-1, entre 2^64-1 et 2^80-1 avec préfixe minimum de 48 bits |
| Auto-configuration            | Non implémentée                                       | Implémentée                                                                        |

---

### Remarques

> En IPv6, toutes les communications ne sont pas chiffrées, et la mobilité (réseau mère et réseau hôte) peut poser des problèmes.  
> **Anycast** : Utilisé pour joindre une entité spécifique dans un groupe.

---

### Classes d'adressage IPv4

| Classe       | Plage d’adresses         | Réseau                 | Interface               | Nombre d'identifiants unicast   |
|--------------|---------------------------|------------------------|-------------------------|---------------------------------|
| Classe A     | `0 <= X <= 127`          | X (Réseau) / 0.0.0 et 255.255.255 | Y.Z.K (Interface)     | 2^24 - 2                       |
| Classe B     | `128 <= X <= 191`        | X.Y (Réseau) / 0.0 et 255.255 | Z.K (Interface)       | 2^16 - 2                       |
| Classe C     | `192 <= X <= 223`        | X.Y.Z (Réseau) / 0 et 255   | K (Interface)           | 2^8 - 2                        |
| Classe D     | `224 <= X <= 239`        | Multicast              | -                       | -                               |
| Classe E     | `240 <= X <= 255`        | Expérimental           | -                       | -                               |

---

### Notes supplémentaires

- Les identifiants **Loopback** (0.0.0) sont confondus avec les identifiants réseau.
- Si toute la partie interface est à zéro, l'adresse correspond à un **Anycast**.
- Si le préfixe commence par `FF`, l’adresse est un **Multicast**.
- **Unicast** : toutes les autres adresses non mentionnées précédemment.

---

### Adressage IPV6

| 64bits  | 64 bits   |
| ------- | --------- |
| préfixe | interface |
# Adresse IPv6
| Type d'adresses | Sous catégorisation     | Caractéristique                                                                                                |
| --------------- | ----------------------- | -------------------------------------------------------------------------------------------------------------- |
| anycast         | Interface=0             |                                                                                                                |
| multicast       | Préfixe commence par FF | permanente `0000` FF0000                                                                                       |
| multicast       | Préfixe commence par FF | temporaire    `0001` FF0001                                                                                    |
| multicast       | Préfixe commence par FF | de site local le scope est egal à `101` FF0000101                                                              |
| unicast         | Adresse IPv4 mappée     | Compatible avec IPv4, les 96 premiers bits sont à  0 les 64 premiers du préfixe suivi des 32 bits d'interfaces |
| unicast<br>     | Unicast de lien local   | Communication locale, commence par `FE8`                                                                       |
| unicast<br>     | Unicast de site local   | Communication locale, commence par `FEC`                                                                       |
| unicast<br>     | Unicast global          | `autres`                                                                                                       |

# Routage IPV6 vs Routage IPV4

| Protocole     | IPv4         | IPv6                |
|---------------|--------------|---------------------|
| Protocoles    | BGP, OSPF    | BGP4+, OSPFv6      |
| En-tête       | Variable     | Fixe, simplifiée    |
| Fragmentation | Possible     | Pas possible        |
| Auto-config   | non implémentée | implémentée     |
