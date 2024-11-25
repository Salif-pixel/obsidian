
---



## 1. Entropie

L'entropie mesure l'incertitude ou la pureté d'un ensemble de données. Elle est calculée par la formule suivante :

$$
E(S) = - \sum_{i=1}^{n} p_i \cdot \log_2(p_i)
$$

Dans notre cas, nous avons les occurrences suivantes pour chaque classe :
- **Bus** : 4 occurrences
- **Train** : 3 occurrences
- **Car** : 3 occurrences

### Calcul des probabilités pour chaque classe

- $$ p(\text{Bus}) = \frac{4}{10} = 0.4 $$
- $$ p(\text{Train}) = \frac{3}{10} = 0.3 $$
- $$ p(\text{Car}) = \frac{3}{10} = 0.3 $$

### Application de la formule de l'entropie

L'entropie totale de l'ensemble initial est donc :

$$
E(\text{total}) = - (0.4 \cdot \log_2(0.4) + 0.3 \cdot \log_2(0.3) + 0.3 \cdot \log_2(0.3)) \approx 1.571
$$

# arbre non binaire

## 2. Gain d'information

Le gain d'information est la différence entre l'entropie de l'ensemble initial \(E(S)\) et l'entropie conditionnelle de cet ensemble après division par l'attribut "Income level".

$$
\text{Gain d'information} = E(S) - E(S | \text{Attribut})
$$

### Calcul de l'entropie pour chaque sous-ensemble

#### 1. Pour "Income Level" = low

1. Sous-ensemble : **Bus, Bus**
2. Occurrences de chaque type de transport :
   - **Bus** : 2 occurrences
3. Probabilités pour chaque type de transport :
   - $$ p(\text{Bus}) = \frac{2}{2} \approx 1 $$
4. Calcul de l'entropie :
   $$
   E(\text{income level = low}) = - (1 \cdot \log_2(1) )=0
   $$

5. Entropie pour "Income level" = low :
   $$
   E(\text{Income level = low}) \approx 0
   $$

#### 2. Pour "Income Level" = medium

1. Sous-ensemble : **Bus, Bus,Train, Train,Train, Car**
2. Occurrences de chaque type de transport :
   - **Bus** : 2 occurrence
   - **Train** : 3 occurrences
   - **Car** : 1 occurrence
3. Probabilités pour chaque type de transport :
   - $$ p(\text{Bus}) = \frac{2}{6} = 0.333 $$
   - $$ p(\text{Train}) = \frac{3}{6} = 0.5 $$
   - $$ p(\text{Car}) = \frac{1}{6} = 0.166 $$
4. Calcul de l'entropie :
   $$
   E(\text{income level =medium}) = - (0.333 \cdot \log_2(0.333) + 0.5 \cdot \log_2(0.5) + 0.166 \cdot \log_2(0.166))
   $$
5. Résultat des termes :
- $$( 0.333 \cdot \log_2(0.333) = -0.528 )$$
   - $$( 0.166 \cdot \log_2(0.166) = -0.43 )$$
   - $$( 0.5 \cdot \log_2(0.5) = -0.5 )$$
7. Entropie pour " income level" =medium:
   $$
   E(\text{income level =medium}) = 1.45
   $$



#### 3. Pour "income level" = high

1. Sous-ensemble : **Car, Car**
2. Occurrences de chaque type de transport :
   - **Car** : 2 occurrences
3. Probabilités pour chaque type de transport :
   $$ p(\text{Car}) = 1 $$
4. Calcul de l'entropie :
   $$
   E(\text{income level =high}) = - (1 \cdot \log_2(1)) = 0
   $$

### Entropie pondérée

Pour obtenir l'entropie conditionnelle pondérée, nous calculons la moyenne pondérée des entropies de chaque sous-ensemble :

$$
E(\text{pondéré}) = (0.6 \cdot 1.45) + (0.2 \cdot 0) + (0.2 \cdot 0) = 0,87
$$

### Calcul du gain d'information

Le gain d'information est alors :

$$
\text{Gain d'information} = E(\text{total}) - E(\text{pondéré}) = 1.571 - 0,87 = 0.701
$$
---
# arbre binaire
## 2. Gain d'information

Le gain d'information est la différence entre l'entropie de l'ensemble initial \(E(S)\) et l'entropie conditionnelle de cet ensemble après division par l'attribut "Income level".

$$
\text{Gain d'information} = E(S) - E(S | \text{Attribut})
$$

### Calcul de l'entropie pour chaque sous-ensemble

#### 1. Pour "Income Level" = Hight & Low

1. Sous-ensemble : **Bus, Bus,Car,Car**
2. Occurrences de chaque type de transport :
   - **Bus** : 2 occurrences
3. Probabilités pour chaque type de transport :
   - $$ p(\text{Bus}) = \frac{2}{4} \approx 0.5 $$
   - - $$ p(\text{Car}) = \frac{2}{4} \approx 0.5 $$
1. Calcul de l'entropie :
   $$
   E(\text{income level = low  High}) = - (0.5 \cdot \log_2(0.5)+0.5 \cdot \log_2(0.5) )=1
   $$

5. Entropie pour "Income level" = low & High :
   
   $$
   E(\text{Income level = low high}) \approx 1
   $$

#### 2. Pour "Income Level" = medium

1. Sous-ensemble : **Bus, Bus,Train, Train,Train, Car**
2. Occurrences de chaque type de transport :
   - **Bus** : 2 occurrence
   - **Train** : 3 occurrences
   - **Car** : 1 occurrence
3. Probabilités pour chaque type de transport :
   - $$ p(\text{Bus}) = \frac{2}{6} = 0.333 $$
   - $$ p(\text{Train}) = \frac{3}{6} = 0.5 $$
   - $$ p(\text{Car}) = \frac{1}{6} = 0.166 $$
4. Calcul de l'entropie :
   $$
   E(\text{income level =medium}) = - (0.333 \cdot \log_2(0.333) + 0.5 \cdot \log_2(0.5) + 0.166 \cdot \log_2(0.166))
   $$
5. Résultat des termes :
- $$( 0.333 \cdot \log_2(0.333) = -0.528 )$$
   - $$( 0.166 \cdot \log_2(0.166) = -0.43 )$$
   - $$( 0.5 \cdot \log_2(0.5) = -0.5 )$$
7. Entropie pour " income level" =medium:
   $$
   E(\text{income level =medium}) = 1.45
   $$




### Entropie pondérée

Pour obtenir l'entropie conditionnelle pondérée, nous calculons la moyenne pondérée des entropies de chaque sous-ensemble :

$$
E(\text{pondéré}) = (0.6 \cdot 1.45) + (0.4 \cdot 1) = 1.27
$$

### Calcul du gain d'information

Le gain d'information est alors :

$$
\text{Gain d'information} = E(\text{total}) - E(\text{pondéré}) = 1.571 - 1.27 = 0.301
$$
---
