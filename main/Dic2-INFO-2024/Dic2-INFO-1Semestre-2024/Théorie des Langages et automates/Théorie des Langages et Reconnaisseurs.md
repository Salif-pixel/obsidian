

---



## Symboles, Alphabets et Mots
- **Symbole** : Élément indivisible servant de brique de base pour concevoir un mot.
- **Alphabet** : Ensemble fini et non vide de symboles. Un alphabet ne peut pas être infini.
- **Mot** (ou chaîne) : Suite de symboles appartenant à un alphabet. Les mots sont mis bout à bout, et il ne peut pas y avoir d'espaces dans un mot, sauf si l'espace est spécifié comme un symbole de l'alphabet.

Un mot possède une longueur notée `|m|`, qui correspond au nombre de symboles dans le mot.  
Par exemple, `|000110| = 6`.

- **Notation `|m|s`** : Nombre de fois qu’un symbole `s` apparaît dans un mot `m`, noté `|m|s = n`, avec `0 <= n <= |m|`.

### Le Mot Vide 
- **Epsilon (ε)** : Représente le mot vide.
- `i-ème` **Symbole** : Position du symbole à l’index `i` dans un mot `m`, tel que `1 < i < |m|`.
    - Exemple : dans `0001001`, `m[3] = 0`, `m[4] = 1`.

### Puissance d'un Alphabet
- La puissance d’un alphabet désigne l'ensemble de tous les mots de longueur `k`.
- **Sigma étoile (Σ*)** : L’ensemble des mots de longueur de 0 à l'infini, incluant `{ε, 0, 00, 10, 110, 000}`, défini comme `Σ* = Σ^0 U Σ+`.

On peut **concaténer** deux mots d’un alphabet, par exemple :
- Si `A = a1...an` et `B = b1...bn`, alors `AB = a1...anb1...bn`.

### Facteur de Mots
Les mots `A`, `B`, et `C` sont définis sur l'alphabet `Σ`. Un mot `B` est un facteur (ou sous-chemise) du mot `ABC` si `B` est une séquence que l'on peut extraire de `ABC`.

## Langage
Un **langage** est un ensemble de mots construits sur un alphabet, donc une partie de `Σ*`.

### Langages Particuliers
- **Langage de Tout Alphabet** : L'ensemble des mots construits sur un alphabet donné.
- **Langage Vide** : Contient absolument rien.
- **Langage du Mot Vide** : Contient uniquement le mot vide (ε).

## Tête de Lecture
La **case courante** est la position actuelle de la tête de lecture. Un **reconnaisseur à sens unique** déplace la tête dans une seule direction : soit vers la gauche, soit vers la droite, ou reste sur place.
## La mémoire auxiliaire
la mémoire peut  prendre des formes différentes elle assurent deux fonctions:
- une fonction de correspondance 
- une fonction de transition
## Unité de  contrôle
 Elle est le cœur du reconnaisseur elle dicte au reconnaisseur son comportement
 elle décide du déplacement a effectue d'un état `ei `a `ej` ou d'un état `ei` a `ei`
## Fonctionnement d'un reconnaisseur

Un reconnaisseur opère par des séquences  de déplacements , la case courante et  l'état de la mémoire  sont évalué par la fonction de transition
## La configuration
C'est une cartographie du reconnaisseur décrivant :

**l'état de l'unité de contrôle**
- le contenu de la bande de lecture
- la position de la tet de lecture
- le contenu de la mémoire 

## les types de reconnaisseurs

### Reconnaisseur Déterministe
A chaque configuration pour tout symbole , un et un seul déplacement est possible au plus
`ei `--ai-->`ej` on a un seul déplacement pour un symbole ai
### Reconnaisseur Non Déterministe
on ne connait pas le bon chemin
`ei `--ai-->`ej`  
`ej` --ai-->`ei`
`ei` --ai-->`ei`  

## Type de configurations particulières

### Configuration initial
elle est défini `état initial`  l'état initial est unique la tête de lecture est sur la case positionner le plus gauche
### Configuration finale
elle est défini `état final`  parmi tous les états on peut avoir plusieurs états finaux il faut que tout le mot soit lu c'est a dire la tête de lecture se place sur le symbole le plus a droite pour cela  il faut que le reconnaisseur se place sur l'un deux et la mémoire doit être dans une configuration satisfaisante considère comme mémoire finale

## Condition d'acceptation
Soit m un mot on quitte une configuration initiale  et effectue une séquence de déplacements successifs qui termines sur une configuration finale `Ci--> c1,C2,Cf`
## Example
###  Vérification du mot "`ababaa`" dans le langage L

Soit le langage **L** défini par le reconnaisseur ci-dessous. Vérifions si le mot "`ababaa`" ∈ L.

#### Tableau des transitions du reconnaisseur

| État | Entrée | État suivant | Sortie      |
| ---- | ------ | ------------ | ----------- |
| 0    | a      | 1            | (0, ababaa) |
| 1    | b      | 0            | (1, babaa)  |
| 0    | a      | 1            | (0, abaa)   |
| 1    | b      | 0            | (1, baa)    |
| 0    | a      | 1            | (0, aa)     |
| 1    | a      | 0            | (0, a)      |
| 0    | ε      | 1            | (0, ε)      |

#### Dérivation du mot "`ababaa`"

1. **État initial** : 0
   - Lire **a**, transition vers l'état 1 : (0, `ababaa`) 
2. **État actuel** : 1
   - Lire **b**, transition vers l'état 0 : (1, `babaa`) 
3. **État actuel** : 0
   - Lire **a**, transition vers l'état 1 : (0, `abaa`) 
4. **État actuel** : 1
   - Lire **b**, transition vers l'état 0 : (1, `baa`) 
5. **État actuel** : 0
   - Lire **a**, transition vers l'état 1 : (0, `aa`) 
6. **État actuel** : 1
   - Lire **a**, transition vers l'état 0 : (1, `a`) 
7. **État actuel** : 0
   - Lire **ε**, transition vers l'état 0 : (0,ε )

### Conclusion

Le mot "`ababaa`" peut être dérivé en suivant les transitions du reconnaisseur et termine dans l'état 0, indiquant que **ababaa** ∈ L.

---
[[Grammaire de réécriture]]