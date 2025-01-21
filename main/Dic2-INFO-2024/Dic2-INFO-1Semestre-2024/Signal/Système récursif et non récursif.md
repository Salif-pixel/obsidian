# Traitement du Signal

## Concepts de Base

- **Signal** : 
  $$ e \geq 2f_{\text{max}} $$
  - Une période rapprochée permet de ne pas perdre l'information.

- **Domaines** : 
  - **Domaine temporel** : Signaux évoluant en fonction du temps.
  - **Domaine fréquentiel** : Les signaux peuvent être analysés en fréquence.

- **Écoute et Parole** : 
  - L'être humain parle dans le temps mais écoute dans la fréquence.

---

## Transformée de Fourier

- Pour effectuer un traitement de signal, il est essentiel de passer du domaine temporel au domaine fréquentiel, surtout en cas de superposition.
- **Transformée de Fourier** : Change un signal du domaine temporel au domaine fréquentiel.
- La représentation d'un signal dans le domaine fréquentiel est appelée **spectre**.
- Un signal continu dans le domaine fréquentiel devient périodique.
- Un signal échantillonné en temps a un spectre qui est périodique en fréquence.

---

## Échantillonnage

- **Sur-échantillonnage** : Si \( $$f_e > 2f_{\text{max}} $$\), les bandes sont largement séparées, entraînant un gaspillage de la bande passante.
- **Échantillonnage critique** : Si \( $$f_e = 2f_{\text{max}}$$ \), les bandes se touchent à leurs limites.
- **Sous-échantillonnage** : Si \($$ f_e < 2f_{\text{max}}$$ \), il y a chevauchement de bandes, ce qui entraîne une très mauvaise qualité.

---

## Systèmes

- **Définition d'un système** : Un ensemble cohérent d'éléments interdépendants.
- **Système discret** : Prend en entrée un signal discret et la sortie est également un signal discret.
- **Système continu** : Fonctionne de la même manière, mais avec des signaux continus.
- **Système linéaire** : 
  - **Additif** : La somme des signaux à l'entrée reste la même à la sortie.
  - **Homogène** : Multiplier un signal à l'entrée par un facteur équivaut à multiplier la sortie par le même facteur.
- **Système invariant** : le décalage a l'entrée est la même a la sortie


---

## Composants d'un Filtre

- **Additionneur** : Prend deux signaux et les additionne.
- **Multiplieur** : 
  - Multiplie un signal par un autre ou par un facteur.
  - Si le facteur est inférieur à 1, il atténue; s'il est supérieur à 1, il amplifie.
- **Cellule mémoire** : Retarde le signal.

---

## Concept de Soustraction

- Un soustracteur peut être conçu avec un multiplieur, en multipliant par -1 et en utilisant un additionneur.

---

## Représentations

| Composant       |     | Sorties               |     | Symbole   |     |     |
| --------------- | --- | --------------------- | --- | --------- | --- | --- |
| Multiplieur     |     | $$ As(n) $$           |     | Triangle  |     |     |
| Additionneur    |     | $$ s_1(n) + s_2(n) $$ |     | Cercle    |     |     |
| Cellule mémoire |     | $$ s(n-1) $$          |     | Rectangle |     |     |


---

## Filtre Numérique

- On peut retarder le son et l'additionner pour créer un écho.
- **Équation aux différences** : Relation qui relie le signal d'entrée au signal de sortie dans un système discret.

---

## Systèmes Récursifs

- Un **système récursif** est un système dont la sortie est réinjectée dans le système.
- **Réponse impulsionnelle** : La réponse obtenue lorsque l'entrée est un Dirac.
  - \( $$g(n) = 2s(n) - \frac{1}{2}s(n-1)$$ \)
  - La réponse impulsionnelle : \( $$h(n) = 2 \cdot \text{Dirac}(n) - \frac{1}{2} \cdot \text{Dirac}(n-1)$$ \)

---

## Filtres

- **Filtres non récursifs** : La réponse est non finie.
- **Filtres récursifs** : La réponse est infinie.
