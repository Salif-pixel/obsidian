
---

# Langages formels et leurs hiérarchies



### Alphabet et mots

- **Alphabet simple (Σ):** Un ensemble fini de symboles, par exemple Σ = {0, 1}.
- **Mot:** Une séquence finie de symboles d'un alphabet. Par exemple, 01, 10, 00 sont des mots sur l'alphabet {0, 1}.

### Langages

Un langage est un ensemble de mots.

#### Exemples de langages

- **Langage des mots de longueur 2 sur Σ = {0, 1}:** `{00, 01, 10, 11}`
- **Langage des mots de longueur paire sur Σ = {0, 1}:** `{ε, 00, 0101, 1100, ...} `(ε représente le mot vide)

### Hiérarchie de Chomsky

La hiérarchie de Chomsky est une classification des langages formels en quatre familles principales :

1. **Langages réguliers:**
- Les plus simples des langages formels.
- Peuvent être reconnus par des automates finis.
- Exemples : les expressions régulières, les langages de mots finis sur un alphabet fini.
2. **Langages algébriques:**
- Plus expressifs que les langages réguliers.
- Peuvent être générés par des grammaires algébriques.
- Exemples : les langages de parenthèses bien formées, les langages générés par les expressions arithmétiques simples.
3. **Langages contextuels:**
- Plus expressifs que les langages algébriques.
- Peuvent être générés par des grammaires contextuelles.
4. **Langages généraux:**
- La famille la plus large de langages formels.
- Peuvent être reconnus par des machines de Turing.

# Langages réguliers

-> On appelle Langage Régulier pour Σ
1. ∅ (l'ensemble vide) est un langage régulier pour Σ 
2. ε est un langage régulier pour Σ 
3. ∀ a ∈ Σ, {a}* est régulier 
4. Soient P et Q deux langages réguliers pour Σ -> P ∪ Q est régulier -> P.Q est régulier -> P* est régulier 
- Rien d'autre n'est régulier


### Exemple 1 :

Pour tout mot u appartenant à Σ* (l'ensemble de toutes les chaînes de caractères possibles sur l'alphabet Σ), le langage {u} est régulier.

- Si u s'écrit` a₁a₂...an`, alors le langage {u} s'écrit comme suit : `{u} = {a₁}{a₂}...{an}`.
- {u} est donc régulier car chaque {aᵢ} l'est (où i varie de 1 à n).
- L'ensemble des langages réguliers est clos pour la concaténation.

### Exemple 2 :

Tout langage fini est régulier.

- Soit L un langage fini.
- L'ensemble des mots finis de L =` {u₁, u₂, ..., uk}` s'écrit : L =` {u₁} ∪ {u₂} ∪ ... ∪ {uk}`.
- L est régulier car chaque {uᵢ} l'est (où i varie de 1 à k).
- L'ensemble des langages réguliers est clos pour l'union.
- 
### Exemple 3 : L'ensemble de tous les mots, Σ* est régulier

- Soit Σ = `{a₁, ..., aₚ}`
- Le langage `{a₁, ..., aₚ}`_ est régulier car:_*
    - Il n'est rien d'autre que la fermeture de Kleene de ce langage.
    - Donc Σ* est un langage régulier car ces derniers sont clos pour cette opération.

### Exemple 4 : Sur l'alphabet {a, b}, l'ensemble {aⁿbⁿ | n ∈ ℕ} est régulier

- __Le langage {aⁿ | n ∈ ℕ} = a_ est régulier :_*
    - Car fermeture de Kleene du langage régulier {a}.
- __Le langage {bⁿ | n ∈ ℕ} = b_ est régulier :_*
    - Car fermeture de Kleene du langage régulier {b}.
- **Donc, le langage {aⁿbⁿ | n ∈ ℕ}, étant une concaténation des précédents, est donc régulier.**

#### Définition
1. **∅** est une expression régulière dénotant le langage vide ∅.
2. **Σ** est une expression régulière dénotant le langage `{a₁, a₂, ..., aₚ}`.
3. **a ∈ Σ** est une expression régulière qui dénote {a}.
4. Soient P et Q deux expressions régulières qui dénotent respectivement les langages P et Q.
    - **(P + Q)** est une expression régulière qui dénote le langage P ∪ Q.
    - **PQ** est une expression régulière qui dénote le langage P.Q.
    - **(P)*** est une expression régulière qui dénote P*.
- Rien d'autres n'est régulier

#### Notation
Soit E une expression régulière L (E) est le langage régulier dénoté par E

##### Exemple
E =0 + (1(O)* )
L(E)= {0,1,10,100,100,...}



---


### Équivalence

Deux expressions régulières E′E' et EE sont dites **équivalentes** si :  
L(E)=L(E′)L(E) = L(E')  
C'est-à-dire que les langages définis par EE et E′E' contiennent exactement les mêmes mots.

### Priorité des opérateurs

Les opérateurs dans les expressions régulières suivent cet ordre de priorité :

1. **`*` (étoile de Kleene)** : Plus prioritaire.
2. **`.` (concaténation)** : Moyennement prioritaire.
3. **`+` (union)** : Moins prioritaire.
 `* > . > +`
`0 + (1(0)*) = 0+10*`

Exemple :  
$$0+(1(0)^∗) =0+ 1⋅(0)^∗$$

---

### Exemples expliqués

1. **01**
    
    $$L(01)={}\{ m \in \{0, 1\}^* \mid m \text{ est exactement } 01 \}$$
2. **0*
    
    $$L(0^∗)={}\{ m \in \{0\}^* \mid m \text{ est constitué uniquement de 0 ou de  } \epsilon \}$$
3. **0∗10*
    
    $$L(0∗10^∗)={}\{ m \in \{0, 1\}^* \mid m \text{ contient exactement un } 1 \}$$
4. **(0+1)1(0+1)**
    
    $$L((0+1)1(0+1))={} \{ m \in \{0, 1\}^* \mid m \text{ contient au moins un } 1 \}$$
5. **(0+1)110**
    
    $$L((0+1)110)=\{ m \in \{0, 1\}^* \mid m \text{ se termine par } 110 \}$$
6. **(0+1)* 101 (0+1)* 
	$$ L((0+1)^\ast \, 101 \, (0+1)^\ast) = \{ m \in \{0,1\}^\ast \mid m \text{ contient le facteur } 101 \}  $$
7. **((0+1)(0+1))*
	$$ L(((0+1)(0+1))^\ast) = \{ m \in \{0,1\}^\ast \mid m \text{ est de longueur paire} \} $$


## Equivalence ou égalité
1. Au moins une expression régulière dénotant tout langage régulier
2. Possible de construire un langage régulier dénoté par une expression régulière 
3. pour tout langage régulier il existe une infinité d'expressions régulières
4. deux expressions réguliers sont équivalentes `ssi ` elles dénotent le même langage


## Quelques Propriétés

## Propriétés principales
1. $$ \alpha + (\beta + \gamma) \equiv  (\alpha + \beta) + \gamma $$
2. $$ \alpha + \beta \equiv  \beta + \alpha $$
3. $$ \alpha + \phi \equiv  \alpha $$
4. $$ \alpha + \alpha \equiv  \alpha $$
5. $$ \alpha \cdot (\beta \gamma) = (\beta \alpha)\cdot \gamma $$
6. $$ \alpha \cdot \epsilon = \epsilon \cdot \alpha = \alpha $$
7. $$ \alpha \cdot (\beta + \gamma) = \alpha \beta + \alpha \gamma $$
8. $$ (\alpha + \beta) \cdot \gamma = \alpha \gamma + \beta \gamma $$

## Propriétés avancées
9. $$ \phi \cdot \alpha \equiv \alpha \cdot \phi \equiv \phi $$
10. $$ \phi^\ast \equiv \epsilon $$
11. $$ (\alpha^\ast)^\ast \equiv \alpha^\ast $$

[[Présentation des automates finis]]