

### Réseau représenté :

- Machine MA : IP 193.2.2.2
- Machine MB : IP 193.8.8.8
- Routeur R1 :
    - Interface `eth0` : 193.2.2.1
    - Interface `eth1` : 193.5.5.4
- Routeur R2 :
    - Interface `eth0` : 193.5.5.5
    - Interface `eth1` : 193.8.8.6

Les machines MA et MB sont dans des sous-réseaux différents. La communication nécessite le routage via R1 et R2.

#### Pour la machine MA :

| Destination | Passerelle | Interface | Saut |
| ----------- | ---------- | --------- | ---- |
| R1          | -------    | eth0      | 0    |
| R2          | 193.2.2.3  | eth0      | 1    |
| MB          | 193.2.2.3  | eth0      | 2    |

#### Pour le routeur R1 :

| Destination  | Passerelle | Interface | Saut |
| ------------ | ---------- | --------- | ---- |
| 193.2.2.0/24 | 193.2.2.3  | eth0      | 1    |
| 193.5.5.0/24 | 193.5.5.4  | eth1      | 1    |
| 193.8.8.0/24 | 193.5.5.5  | eth1      | 2    |

#### Pour le routeur R2 :

| Destination | Passerelle | Interface | Saut |
| ----------- | ---------- | --------- | ---- |
| MA          | 193.5.5.5  | eth0      | 1    |
| MB          | ------     | eth1      | 0    |
| R1          | 193.5.5.5  | eth0      | 0    |

#### Pour la machine MB :

| Destination | Passerelle | Interface | Saut |
| ----------- | ---------- | --------- | ---- |
| R1          | 193.8.8.6  | eth0      | 1    |
| R2          | -------    | eth0      | 0    |
| MA          | 193.8.8.6  | eth0      | 2    |

