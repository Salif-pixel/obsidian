
---
# Contexte
Oui : Le mot est accepté → un mot du langage
Non : Le mot n'est pas accepté → il n'appartient pas au langage

## Deux types d'automates

### Automates finis déterministes (AFD)
- Il n'y a pas de transitions étiquetées ε.
- Il y a une transition pour chaque état et chaque symbole.

### Automates finis non déterministes (AFN)
1. Une transition peut être étiqueté ε.
2. Plus d'une transition possible pour un symbole de l'alphabet.

# Automate finis non déterministe

Un **automate fini non déterministe (AFN)** est défini comme un 5-uplet :  
**⟨Q, Σ, δ, q₀, F⟩**, où :

1. **Q** : Ensemble des états
2. **Σ** : Alphabet d’entrée
3. **δ** : Fonction de transition  
   δ : Q × (Σ ∪ {ε}) → 𝒫(Q)
4. **q₀ ∈ Q** : État initial
5. **F ⊆ Q** : Ensemble des états d’acceptation

# Configuration et mouvement d’un automate

## Définition de l’automate
Un automate est défini comme :  
**𝒜 = ⟨Q, Σ, δ, q₀, F⟩**

## Configuration
Une configuration est un couple :  
**(q, m) ∈ Q × Σ\***, où :  
- **q** : État courant de l’automate  
- **m** : Partie du mot à reconnaître qui n’a pas encore été lue  

### Configurations particulières :
- **Configuration initiale** : **(q₀, m)**  
- **Configuration finale** : **(q,ε) ∈ F**

---

## Mouvement (aussi appelé transition)
Un mouvement correspond :  
- Au déplacement de la tête de lecture  
- À la lecture d’un symbole  

Notation :  
**(q, am) ⊢ (q', m)**, où :  
- **q' = δ(q, a)**

# Table de transition

## Définition
- Les **lignes** de la table correspondent aux **états**.  
- Les **colonnes** correspondent aux **symboles d’entrée** et à **ε** (transition vide).  
- **Entrée** : Un couple (état, symbole) donne un ensemble d’états (résultat de la fonction de transition).  
- Si la fonction de transition ne donne aucun résultat, le couple est invalide.

---

## Exemple de table de transition
Table pour l’AFN de l’exemple :  

| État | a      | b   | ε   |
| ---- | ------ | --- | --- |
| 0    | {0, 1} | ∅   | {2} |
| 1    | ∅      | {2} | ∅   |
| 2    | ∅      | ∅   | {3} |
| 3    | ∅      | ∅   | ∅   |

---

## Points importants
- Permet de **trouver facilement les transitions** à partir du couple (état, entrée).  
- Montre que la **plupart des états** peuvent ne pas avoir de transition sortante.
