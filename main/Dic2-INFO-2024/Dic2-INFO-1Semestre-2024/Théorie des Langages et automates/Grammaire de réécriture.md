
---


## Définition des Grammaires

Les grammaires sont la classe la plus importante de générateur de langage.

- **Grammaire** : un système mathématique permettant de générer tous les mots d’un langage.
- Pour un langage **L**, une grammaire se fonde sur deux ensembles disjoints de symboles :
  1. **L'ensemble des symboles non terminaux (N)** : appelé alphabet non terminal.
     - Les non terminaux représentent les symboles élémentaires du langage défini par la grammaire.
  2. **L'ensemble des symboles terminaux (Σ)** : appelé alphabet terminal.
     - Les terminaux représentent des mots constitués de non terminaux et sont utilisés dans la génération des mots du langage.
---

## Cœur d’une Grammaire

Le cœur d’une grammaire est un ensemble fini, noté **P**, de règles de production (ou production).

- **Règles de production** : décrivent comment une phrase du langage définie par une grammaire va être générée.
- Une règle de production **(a, b)** (ou règle de réécriture) est un élément de l’ensemble **P**.
- Notations :
  - **(N ∪ Σ)***N (N ∪ Σ)* ⇥ (N ∪ Σ):
    1. **(N ∩ Σ)***N (N ∪ Σ)* : désigne n’importe quelle chaîne contenant au moins un non terminal.
    2. **(N ∪ Σ)*** : désigne n’importe quelle chaîne.


### Convention

- Si **(a, b)** est une règle de production, alors la notation suivante est utilisée : **a → b**.
---
## Grammaire de Réécriture

Une grammaire de réécriture est un 4-uplet noté **(N,Σ , P, S)** où :

- **N** : un ensemble fini de symboles non terminaux, appelé l'alphabet non terminal.
- **Σ** : un ensemble de symboles terminaux, appelé alphabet terminal, tel que **N ∩ Σ ≠ ∅**.
- **P** : un sous-ensemble fini de :
  - **(N ∪ Σ)*N (N ∪ Σ)* ⇥ (N ∪ Σ)***
  - Un élément **(a, b) ∈ P**, noté **a → b**, est une règle de production.
- **S** : un élément de **N** appelé l’axiome de la grammaire.
## Exemple 

Soit le langage **L** défini par la grammaire suivante :

- **G** = (N, T, P, S) = 
  - N = {P, I}
  - T = {a, b}
  - P = {`P → e, P → aI, P → bI, I → aP, I → bP`}
  - S = P

### Vérification du mot "`ababaa`" ∈ L

Nous allons montrer que "`ababaa`" peut être généré par la grammaire en utilisant les règles de production. Voici le tableau des étapes de dérivation :

| Étape | Production | Résultat |
| ----- | ---------- | -------- |
| 1     | P → aI     | aI       |
| 2     | I → bP     | abP      |
| 3     | P → aI     | abaI     |
| 4     | I → bP     | ababP    |
| 5     | P → aI     | ababaI   |
| 6     | I → e      | ababaa   |

### Conclusion

Le mot "`ababaa`" appartient bien au langage **L**, car il peut être dérivé à partir de l'axiome **P** en appliquant les règles de production de la grammaire.

---
[[Les expressions régulières]]