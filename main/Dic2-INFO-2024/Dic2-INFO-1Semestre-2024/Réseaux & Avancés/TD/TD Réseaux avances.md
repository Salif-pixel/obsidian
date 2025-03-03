
---
# TD1
## Exercice 2

voici une ip _2001:200:25AF:1400/48_

1. Découpons ce réseau en 8 sous réseaux
on aura 2^3 =<font color="#92d050"> 8   </font>
_2001:200:25AF:(<font color="#de7802"><span style="background:#d3f8b6">000</span>0</font>)000:0000:0000:0000:0000/51_

| <font color="#92d050">0</font>     | 2001 | 200 | 25AF | <font color="#f79646">000</font> | <font color="#f79646">0</font> | 000 |     |
| ---------------------------------- | ---- | --- | ---- | -------------------------------- | ------------------------------ | --- | --- |
| <font color="#92d050">1</font><br> | 2001 | 200 | 25AF | <font color="#f79646">001</font> | <font color="#f79646">0</font> | 000 |     |
| <font color="#92d050">2</font><br> | 2001 | 200 | 25AF | <font color="#f79646">010</font> | <font color="#f79646">0</font> | 000 |     |
| <font color="#92d050">3</font><br> | 2001 | 200 | 25AF | <font color="#f79646">011</font> | <font color="#f79646">0</font> | 000 |     |
| <font color="#92d050">4</font><br> | 2001 | 200 | 25AF | <font color="#f79646">100</font> | <font color="#f79646">0</font> | 000 |     |
| <font color="#92d050">5</font><br> | 2001 | 200 | 25AF | <font color="#f79646">101</font> | <font color="#f79646">0</font> | 000 |     |
| <font color="#92d050">6</font><br> | 2001 | 200 | 25AF | <font color="#f79646">110</font> | <font color="#f79646">0</font> | 000 |     |
| <font color="#92d050">7</font><br> | 2001 | 200 | 25AF | <font color="#f79646">111</font> | <font color="#f79646">0</font> | 000 |     |


voici les 8 sous réseaux  

_2001:200:25AF::/51_
_2001:200:25AF:2000/51:_
_2001:200:25AF:4000/51:_
_2001:200:25AF:6000/51:_
_2001:200:25AF:8000/51:_
_2001:200:25AF:A000/51:_
_2001:200:25AF:C000/51:_
_2001:200:25AF:E000/51:_

2. Quelle est la plage des adresses utilisables pour le sous réseau numero 3 _2001:200:25AF:3400:_

_2001:200:25AF:6000:0000:0000:0000:0001_ à  _2001:200:25AF:7FFF:FFFF:FFFF:FFFF:FFFFF_ 

3. Quelle est la liste des adresses des 16 sous réseaux obtenus a partir du sous réseau numero 6 _2001:200:25AF:C000:/51_
on aura 2^4  =<font color="#92d050"> 16   </font>
_2001:200:25AF:(<font color="#de7802">110<span style="background:#d3f8b6">0000</span>0</font>)00:0000:0000:0000:0000/55_

| <font color="#92d050">0</font>     | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">0000</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| ---------------------------------- | ---- | --- | ---- | -------------------------------- | --------------------------------- | ------------------------------ | --- | ---- | ---- | ---- | ---- |
| <font color="#92d050">1</font><br> | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">0001</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">2</font><br> | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">0010</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">3</font><br> | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">0011</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">4</font><br> | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">0100</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">5</font><br> | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">0101</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">6</font><br> | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">0110</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">7</font><br> | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">0111</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">8</font><br> | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">1000</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">9</font>     | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">1001</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">10</font>    | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">1010</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">11</font>    | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">1011</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">12</font>    | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">1100</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">13</font>    | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">1101</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">14</font>    | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">1110</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">15</font>    | 2001 | 200 | 25AF | <font color="#de7802">110</font> | <font color="#de7802">1111</font> | <font color="#de7802">0</font> | 00  | 0000 | 0000 | 0000 | 0000 |

_2001:200:25AF:C000:0000:0000:0000:0000/55_
_2001:200:25AF:C200:0000:0000:0000:0000/55_
_2001:200:25AF:C400:0000:0000:0000:0000/55_
_2001:200:25AF:C600:0000:0000:0000:0000/55_
_2001:200:25AF:C800:0000:0000:0000:0000/55_
_2001:200:25AF:CA00:0000:0000:0000:0000/55_
_2001:200:25AF:CC00:0000:0000:0000:0000/55_
_2001:200:25AF:CE00:0000:0000:0000:0000/55_
_2001:200:25AF:D000:0000:0000:0000:0000/55_
_2001:200:25AF:D200:0000:0000:0000:0000/55_
_2001:200:25AF:D400:0000:0000:0000:0000/55_
_2001:200:25AF:D600:0000:0000:0000:0000/55_
_2001:200:25AF:D800:0000:0000:0000:0000/55_
_2001:200:25AF:DA00:0000:0000:0000:0000/55_
_2001:200:25AF:DC00:0000:0000:0000:0000/55_
_2001:200:25AF:DE00:0000:0000:0000:0000/55_

4. Quelle est la plage des adresses utilisables pour le sous réseau numero 6 - 3 _2001:200:25AF:C600:0000:0000:0000:0000/55_
_2001:200:25AF:C600:0000:0000:0000:0001/55_  à _2001:200:25AF:C7FF:FFFF:FFFF:FFFF:FFFF/55_

5. Quelle est l'adresse de diffusion du sous réseau numero 6 - 5 il n'en a pas

6.  Quelle est la plage des adresses utilisables pour le sous réseau numero 6 - 14  - 2 voici l'ip 6 - 14 _
 _2001:200:25AF:D(<font color="#de7802">110<span style="background:#d3f8b6">000</span>00</font>)0:0000:0000:0000:0000/58_
on le découpe  en 8 sous réseaux on aura 2^3  =<font color="#92d050"> 8   </font>

| <font color="#92d050">0</font>     | 2001 | 200 | 25AF | D   | <font color="#de7802">110</font> | <font color="#de7802">000</font> | <font color="#de7802">00</font> | 0   | 0000 | 0000 | 0000 | 0000 |
| ---------------------------------- | ---- | --- | ---- | --- | -------------------------------- | -------------------------------- | ------------------------------- | --- | ---- | ---- | ---- | ---- |
| <font color="#92d050">1</font><br> | 2001 | 200 | 25AF | D   | <font color="#de7802">110</font> | <font color="#de7802">001</font> | <font color="#de7802">00</font> | 0   | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">2</font><br> | 2001 | 200 | 25AF | D   | <font color="#de7802">110</font> | <font color="#de7802">010</font> | <font color="#de7802">00</font> | 0   | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">3</font><br> | 2001 | 200 | 25AF | D   | <font color="#de7802">110</font> | <font color="#de7802">011</font> | <font color="#de7802">00</font> | 0   | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">4</font><br> | 2001 | 200 | 25AF | D   | <font color="#de7802">110</font> | <font color="#de7802">100</font> | <font color="#de7802">00</font> | 0   | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">5</font><br> | 2001 | 200 | 25AF | D   | <font color="#de7802">110</font> | <font color="#de7802">101</font> | <font color="#de7802">00</font> | 0   | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">6</font><br> | 2001 | 200 | 25AF | D   | <font color="#de7802">110</font> | <font color="#de7802">110</font> | <font color="#de7802">00</font> | 0   | 0000 | 0000 | 0000 | 0000 |
| <font color="#92d050">7</font><br> | 2001 | 200 | 25AF | D   | <font color="#de7802">110</font> | <font color="#de7802">111</font> | <font color="#de7802">00</font> | 0   | 0000 | 0000 | 0000 | 0000 |
_2001:200:25AF:DC00:0000:0000:0000:0000/58_
_2001:200:25AF:DC40:0000:0000:0000:0000/58_
_2001:200:25AF:DC80:0000:0000:0000:0000/58_
_2001:200:25AF:DCC0:0000:0000:0000:0000/58_
_2001:200:25AF:DD00:0000:0000:0000:0000/58_
_2001:200:25AF:DD40:0000:0000:0000:0000/58_
_2001:200:25AF:DD80:0000:0000:0000:0000/58_
_2001:200:25AF:DDC0:0000:0000:0000:0000/58_

les adresses utilisables du sous réseau 6 - 14 - 2 sont 

_2001:200:25AF:DC80:0000:0000:0000:0001/58_  à  _2001:200:25AF:DCBF:FFFF:FFFF:FFFF:FFFF/58_

7. Quelle est l'adresse de diffusion du  sous réseau 6 - 14 - 5  il n'en a pas

## Exercice 3

mon adresse mac `6e:df:35:ff:9b:26`
divisons le en deux _6e:df:35_ et _ff:9b:26_

on insère _FF:FE_ entre les deux

`6e:df:35:FF:FE:ff:9b:26`

on inverse le 7e bit du 1e octet
_6e -> 01101110 -> 01101100 -> 6C_
on ajoute le préfixe du lien local FE80

`FE80::6Cdf:35FF:FEFF:9b26`

## Exercice 4



### Réseau représenté :

- Machine MA : IP 193.2.2.2
- Machine MB : IP 193.8.8.8
- Routeur R1 :
    - Interface `eth0` : 193.2.2.3
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

| Destination | Passerelle | Interface | Saut |
| ----------- | ---------- | --------- | ---- |
| MA          | 193.2.2.3  | eth0      | 0    |
| MB          | 193.5.5.4  | eth1      | 1    |
| R2          | 193.5.5.4  | eth1      | 0    |

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

# TD2
## Exercice 1
1. pour chaque IP donnons sa classe son masque le netID le host-ID et l'adresse de diffusion
	a. 9.13.103.5
	b. 137.64.32.7
	c.198.4.87.12
	d.192.168.25.10
	e.169.167.202.2

| Adresse       | classe | masque        | NetID        | HostID    | BroadCast       |
| ------------- | ------ | ------------- | ------------ | --------- | --------------- |
| 9.13.103.5    | A      | 255.0.0.0     | 9.0.0.0      | .13.103.5 | 9.255.255.255   |
| 137.64.32.7   | B      | 255.255.0.0   | 137.64.0.0   | .32.7     | 137.64.255.255  |
| 198.4.87.12   | C      | 255.255.255.0 | 198.4.87.0   | .12       | 198.4.87.255    |
| 192.168.25.10 | C      | 255.255.255.0 | 192.168.25.0 | .10       | 192.168.25.255  |
| 169.167.202.2 | B      | 255.255.0.0   | 169.167.0.0  | .202.2    | 169.167.255.255 |
## Exercice 2
On dispose d'une adresse réseau 195.52.150.0

a. la classe de cette adresse est C

b. découpons le réseau 6 sous réseaux
2^3  = 8
195.52.150.<font color="#de7802"><span style="background:#d3f8b6">000</span>00000</font>

| 195 | 52  | 150 | <font color="#de7802">000</font> | <font color="#de7802">00000</font> |
| --- | --- | --- | -------------------------------- | ---------------------------------- |
| 195 | 52  | 150 | <font color="#de7802">001</font> | <font color="#de7802">00000</font> |
| 195 | 52  | 150 | <font color="#de7802">010</font> | <font color="#de7802">00000</font> |
| 195 | 52  | 150 | <font color="#de7802">011</font> | <font color="#de7802">00000</font> |
| 195 | 52  | 150 | <font color="#de7802">100</font> | <font color="#de7802">00000</font> |
| 195 | 52  | 150 | <font color="#de7802">101</font> | <font color="#de7802">00000</font> |
| 195 | 52  | 150 | <font color="#de7802">110</font> | <font color="#de7802">00000</font> |
| 195 | 52  | 150 | <font color="#de7802">111</font> | <font color="#de7802">00000</font> |
dans chaque sous réseau on aura 2^5 - 2 hôtes =  30
le masque sera
255.255.255.224

l'adresse ip 195.52.150.1  fais partit du sous réseau 
195.52.150.0

## Exercice 3

1. L'adresse suivante est elle une adresse globale ?

_3001:2:1:2::4CFE_
cette adresse ip est une adresse globale car elle n'est ni <span style="background:#d3f8b6">multicast</span> elle ne commence pas par `FF` ni <span style="background:#d3f8b6">anycast</span>  toute sa partie interface n'est pas égal a 0 et c'est pas une adresse <span style="background:#d3f8b6">lien local</span> elle commence pas par `FE8` ni un <span style="background:#d3f8b6">site local</span> elle commence pas par `FEC` et enfin ses `96 premiers bits` ne sont  pas égal a 0 donc ce n'est pas aussi une adresse <span style="background:#d3f8b6">ipv4 mappée</span>

2.  Quelle est le TLA de l'adresse suivante ?

_2001:0688:1f80:2000:0203:ffff:0018:ef1e_

on prend 2001 les 13 derniers bits représentent le TLA

001<span style="background:#d3f8b6">0000000000001</span>

## Exercice 4
En fonction de la longueur de leur préfixe donner le réseau d'appartenance de ces adresses

`2001:88:1f80::203:ffff:4c18:ffe1/64`

`2001:bb76:7878:2::/56`

1. pour _2001:88:1f80::203:ffff:4c18:ffe1/64_

voici son préfixe 2001:88:1f80:0000
il appartient a ce réseau  2001:88:1f80::/64

2. pour _2001:bb76:7878:2::/56_

voici son préfixe 2001:bb76:7878:00
il appartient a ce réseau  2001:bb76:7878::/56

Une entreprise reçoit d'un opérateur le préfixe suivant combien de sous réseaux peut-elle créer ?

`2001:0688:1f80::/48`

_2001:0688:1f80_

le Site-level-aggregator ou SLA est code sur 16 bits don on pourrait avoir 2^16 sous réseaux

## Exercice 5 et 6 voir TD1

## Exercice 7
A partir des adresses Mac suivantes construire les adresses lien local auto configurées automatiquement
Récupérer l’adresse MAC de son mobile et le transformer en Ipv6

1. _02-00-4c-4f-4f-50_ _02004c4f4f50_
- on divise en deux on aura
_02004c_ et _4f4f50_
- on insère FF-FE au milieu
_02004cFFFE4f4f50_
- on inverse le 7e bit du premier octet
02 -> 00000010 -> 00000000 -> 00
- on ajoute le préfixe FE80
_FE80::4cFF:FE4f:4f50

2. _00-03-ff-18-cf-1e_ _0003ff18cf1e_
- on divise en deux on aura
_0003ff_ et _18cf1e_
- on insère FF-FE au milieu
_0003ffFFFE18cf1e_
- on inverse le 7e bit du premier octet
00 -> 00000000 -> 00000010 -> 02
- on ajoute le préfixe FE80
_FE80::203:ffFF:FE18:cf1e_

Récupérer l’adresse MAC de son mobile et le transformer en Ipv4

_C6:09:61:D4:F3:C4_

on prend les  derniers octets

61 D4 F3 C4
01100001  11010100  11110011  11000100

97.212.243.196 -> IPV4

# Hint 1

## Exercice 1 
Faire une comparaison succinte sous forme de tableau

| Critères                      | IPv4                                                  | IPv6                                                                               |
| ----------------------------- | ----------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Plage d'adressage             | 32 bits = 2^32                                        | 128 bits = 2^128                                                                   |
| Type de communications        | Unicast, Multicast, Broadcast                         | Unicast, Multicast, Anycast                                                        |
| Notation                      | Décimale pointée                                      | Hexadécimale avec double point (:)                                                 |
| Organisation                  | Classes                                               | Agrégation                                                                         |
| Nombre d’identifiants Unicast | Variable selon la classe et le nombre de sous-réseaux | Minimum 2^64-1 ou ≥ 2^64-1, entre 2^64-1 et 2^80-1 avec préfixe minimum de 48 bits |
| Auto-configuration            | Non implémentée                                       | Implémentée                                                                        |
| Protocoles                    | BGP, OSPF                                             | BGP4+, OSPFv6                                                                      |
| En-tête                       | Variable                                              | Fixe, simplifiée                                                                   |
| Fragmentation                 | Possible                                              | Pas possible                                                                       |
| Auto-config                   | non implémentée                                       | implémentée                                                                        |

## Exercice 2 : QCM

1. Le nombre d'interface d'une adresse ipv4 est fixe `faux`

2. Le codage NRZ est un protocole de couche `Physique`

3. Lequel de ce protocoles depend de la couche transport `UDP` ou `TCP`

4. Le Type de protocole de routage utilise depend de la position du routeur sur le réseau  `Vrai`

## Exercice 3

Quelles primitives de services sont utilisées en mode non connecté ? le role de chacune d'elles

Requête: primitif utilisé par une entité pour envoyer des données sans établir une connexion au préalable

Indication: Primitif utilisé pour notifier la réception des données envoyées

## Exercice 4

_2001:88:1F80::203:FFFF:4C18:FFe1/54_
a. le type de cette adresse est unicast global
b. donnons son réseau d'appartenance
_2001:88:1F80::/54_

## Exercice 5
Déterminons la classe le masque de réseau le netID le hostID et l'adresse de diffusion de cette adresse:

9.13.103.5
149.103.103.5

| Adresse       | Classe | Masque      | NetID       | HostID    | Broadcast       |
| ------------- | ------ | ----------- | ----------- | --------- | --------------- |
| 9.13.103.5    | A      | 255.0.0.0   | 9.0.0.0     | .13.103.5 | 9.255.255.255   |
| 149.103.103.5 | B      | 255.255.0.0 | 149.103.0.0 | .103.5    | 149.103.255.255 |
# Hint 2
## Exercice 1 

Donnons les primitives utilisés
Requête -> indication 

# Exercice 2 voir Hint1

## Exercice 3
les 2 modes d'utilisation d'osi sont

- mode connecté : il y'a établissement de connexion entre les entités avant l'échange de données . On y note 4 primitives principales Requête -> indication -> Réponse -> Confirmation

- mode non connecté: les é entités n'ont pas besoin d'établir une connexion pour s'échanger des données on a 2 primitives 
	Requête -> indication

## Exercice 4
Déterminons la classe le masque de réseau le netID le hostID et l'adresse de diffusion de cette adresse:

9.13.103.5
149.103.103.5

| Adresse     | Classe | Masque      | NetID      | HostID    | broadcast      |
| ----------- | ------ | ----------- | ---------- | --------- | -------------- |
| 9.13.103.5  | A      | 255.0.0.0   | 9.0.0.0    | .13.103.5 | 9.255.255.255  |
| 137.64.32.7 | B      | 255.255.0.0 | 137.64.0.0 | .32.7     | 137.64.255.255 |

## Exercice 5

L'adresse suivante est elle une adresse de lien local ou de site 
elle n'est ni l'un ni l'autre car elle ne commence pas par FEC ou FE8

Quelle est le TLA de l'adresse suivante ?
2001:0688:1F80:2000:0203:FFFF:0018:EF1E

on prend les 13 dernier bits de 2001

001<span style="background:#d3f8b6">0000000000001</span>
LA TLA de l'adresse est 1

En fonction de la longueur de son préfixe donnons son réseau d'appartenance

_2001:88:1F80::203:FFFF:4C18:FFE1/62_

voici le réseau d'appartenance

`2001:88:1F80::/62`



