

## La Mémoire

- **Définition** : C'est un moyen technique de stocker des informations, avec différents niveaux de mémoire :
  - **Mémoire principale (RAM)**
  - **Mémoire secondaire (Disque dur)**
  - **Mémoire tertiaire (Cloud)**
  - **Mémoire cache** : Une mémoire de courte durée pour accélérer les calculs.

---

## Fichiers

- **Définition** : C'est une vue logique, un ensemble/suite de bits (0, 1).
- **Taille page** : Taille de case.
- **Formules** :
  - \($$ F = \frac{T_{\text{block}}}{N_{\text{block}}}$$ \)
  - \( $$N_{\text{block}} = \frac{T_{\text{Fichier}}}{T_{\text{Block}}} = y$$ \)
- **Secteur** : La plus petite surface délimitée que l'on peut avoir dans un disque.
- **Bloc** : Ensemble de \( x \) secteurs consécutifs.

---

## MBR (Master Boot Record)

- Contient le programme qui charge le système, placé au secteur pour limiter le temps d'action.
- **Table de partition** : Indique où démarre et se termine une partition. Une partition est dite active si elle contient un système d'exploitation démarrable.
- Le MBR indique les partitions actives.
- Le fichier **boot** permet de démarrer l'OS.
- Un disque est une armoire physique binaire.

---

## Algorithmes de Fragmentation

- **Types d'algorithmes** :
  - **First Fit**
  - **Next Fit**
  - **Best Fit** : Minimise la fragmentation.
  - **Worst Fit** : Maximise la fragmentation (création de petits espaces libres inutilisables entre les espaces occupés).

---

## Types de Fragmentation

- **Fragmentation interne** : Espace libre dans un bloc qui n'est pas entièrement occupé.
- **Fragmentation externe** : Un ou plusieurs blocs entièrement libres entre des blocs occupés.

---

## Ext4

- **Structures de données** :
  - `/boot` : Descripteur de boot, table des images et différents blocs de données.
  - **Super bloc** ou boot de bloc.
  - **Table des i-nodes** : Permet aux blocs qui ne sont pas dans le même fichier de ne pas se mélanger. Pour chaque fichier, on a un nœud d'index.
  
---

## Formules liées aux i-nodes

| Description             | Formule                                                                                                  |     |
| ----------------------- | -------------------------------------------------------------------------------------------------------- | --- |
| Nombre de blocs         | $$ NB_d = \frac{T_F}{T_{B_d}} $$                                                                         |     |
| Condition sur la taille | $$ T_F \leq 12 \times T_{B_d} $$                                                                         |     |
| Calcul de h             | $$ h = \frac{T_{B_d}}{T_{@}} $$                                                                          |     |
| Accès indirect simple   | $$ T_F \leq 12 \times T_{B_d} + h \times T_{B_d} $$                                                      |     |
| Accès indirect double   | $$ T_F \leq 12 \times T_{B_d} + h \times T_{B_d} + h^2 \times T_{B_d} $$                                 |     |
| Accès indirect triple   | $$ T_{\text{max}} \leq 12 \times T_{B_d} + h \times T_{B_d} + h^2 \times T_{B_d} + h^3 \times T_{B_d} $$ |     |
| Taille max en Ext4      | $$ T_{\text{max}} = 12 \times T_{B_d} + h \times T_{B_d} + h^2 \times T_{B_d} + h^3 \times T_{B_d} $$    |     |
|                         |                                                                                                          |     |
