

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

## 2. Gain d'information

Le gain d'information est la différence entre l'entropie de l'ensemble initial \(E(S)\) et l'entropie conditionnelle de cet ensemble après division par l'attribut "Car ownership".

$$
\text{Gain d'information} = E(S) - E(S | \text{Attribut})
$$

### Calcul de l'entropie pour chaque sous-ensemble

#### 1. Pour "Car ownership" = 0

1. Sous-ensemble : **Bus, Bus, Train**
2. Occurrences de chaque type de transport :
   - **Bus** : 2 occurrences
   - **Train** : 1 occurrence
3. Probabilités pour chaque type de transport :
   - $$ p(\text{Bus}) = \frac{2}{3} \approx 0.667 $$
   - $$ p(\text{Train}) = \frac{1}{3} \approx 0.333 $$
4. Calcul de l'entropie :
   $$
   E(\text{car ownership = 0}) = - (0.667 \cdot \log_2(0.667) + 0.333 \cdot \log_2(0.333))
   $$
5. Résultat des termes :
   - $$( 0.667 \cdot \log_2(0.667) \approx -0.389 )$$
   - $$( 0.333 \cdot \log_2(0.333) \approx -0.530 )$$
6. Entropie pour "Car ownership" = 0 :
   $$
   E(\text{car ownership = 0}) \approx 0.918
   $$

#### 2. Pour "Car ownership" = 1

1. Sous-ensemble : **Bus,Bus, Train, Train, Car**
2. Occurrences de chaque type de transport :
   - **Bus** : 2 occurrence
   - **Train** : 2 occurrences
   - **Car** : 1 occurrence
3. Probabilités pour chaque type de transport :
   - $$ p(\text{Bus}) = \frac{2}{5} = 0.5 $$
   - $$ p(\text{Train}) = \frac{2}{5} = 0.5 $$
   - $$ p(\text{Car}) = \frac{1}{5} = 0.25 $$
4. Calcul de l'entropie :
   $$
   E(\text{car ownership = 1}) = - (0.5 \cdot \log_2(0.5) + 0.5 \cdot \log_2(0.5) + 0.25 \cdot \log_2(0.25))
   $$
5. Résultat des termes :
   - $$( 0.25 \cdot \log_2(0.25) = -0.5 )$$
   - $$( 0.5 \cdot \log_2(0.5) = -0.5 )$$
6. Entropie pour "Car ownership" = 1 :
   $$
   E(\text{car ownership = 1}) = 1.5
   $$

#### 3. Pour "Car ownership" = 2

1. Sous-ensemble : **Car, Car**
2. Occurrences de chaque type de transport :
   - **Car** : 2 Concurrences
3. Probabilités pour chaque type de transport :
   $$ p(\text{Car}) = 1 $$
4. Calcul de l'entropie :
   $$
   E(\text{car ownership = 2}) = - (1 \cdot \log_2(1)) = 0
   $$

### Entropie pondérée

Pour obtenir l'entropie conditionnelle pondérée, nous calculons la moyenne pondérée des entropies de chaque sous-ensemble :

$$
E(\text{pondéré}) = (0.3 \cdot 0.918) + (0.5 \cdot 1.5) + (0.2 \cdot 0) = 1.036
$$

### Calcul du gain d'information

Le gain d'information est alors :

$$
\text{Gain d'information} = E(\text{total}) - E(\text{pondéré}) = 1.571 - 1.036 = 0.534
$$

---
