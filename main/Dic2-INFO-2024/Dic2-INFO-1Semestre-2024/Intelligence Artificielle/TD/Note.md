---

---
---
## Calcul du Gain

Le gain (**balance**) est défini par la formule suivante :

$$
\text{Gain (balance)} = E_0 - E_1 \cdot P_1 - E_2 \cdot P_2
$$

Avec :

$$
\begin{align*}
& P_1 = \frac{13}{30} \\
& P_2 = \frac{17}{30} \\
& E = -\sum_{i} p_i \cdot \log(p_i) \\
& E_0 = -\left(\frac{16}{30} \cdot \log\left(\frac{16}{30}\right) + \frac{14}{30} \cdot \log\left(\frac{14}{30}\right)\right) \approx \text{(0,300064)} \\
& E_1 = -\left(\frac{12}{13} \cdot \log\left(\frac{12}{13}\right) + \frac{1}{13} \cdot \log\left(\frac{1}{13}\right)\right) \approx \text{(0,117776)} \\
& E_2 = -\left(\frac{4}{17} \cdot \log\left(\frac{4}{17}\right) + \frac{13}{17} \cdot \log\left(\frac{13}{17}\right)\right) \approx \text{(0,236949)}
\end{align*}
$$

Remplaçons chaque expression par ses valeurs pour obtenir les résultats des entropies $$E_0, E_1, et  E_2 $$
Le gain (**temps**) est défini par la formule suivante :
$$
\text{Gain (temps)} = E_0 - E_1 \cdot P_1 - E_2 \cdot P_2
$$

Avec :

$$ \begin{align*}  & E_0 = E(9 \text{ oui}, 5 \text{ non}) = -\left(\frac{9}{14} \cdot \log\left(\frac{9}{14}\right) + \frac{5}{14} \cdot \log\left(\frac{5}{14}\right)\right) \\ & E_1 = E(\text{Temps = ens, pluv}) = E(5 \text{ oui}, 5 \text{ non}) = -\left(\frac{5}{10} \cdot \log\left(\frac{5}{10}\right) + \frac{5}{10} \cdot \log\left(\frac{5}{10}\right)\right) \\ & E_2 = E(\text{Temps = couvert}) = E(4 \text{ oui}, 0 \text{ non}) = -\left(\frac{4}{4} \cdot \log\left(\frac{4}{4}\right) + \frac{0}{4} \cdot \log\left(\frac{0}{4}\right)\right) = 0 \end{align*} $$

Le gain (**WH**) est défini par la formule suivante :
$$
\text{Gain (WH)} = E_0 - E_1 \cdot P_1 - E_2 \cdot P_2
$$

$$\begin{align*} & E_0 = E(\text{WHW} <= 2.5)=E(10 \text{ B}, 6 \text{ G}) = -\left(\frac{10}{16} \cdot \log\left(\frac{10}{16}\right) + \frac{6}{16} \cdot \log\left(\frac{6}{16}\right)\right) \\ & E_1 = E(\text{WHW} < 36) = E(1 \text{ B}, 1 \text{ G}) = -\left(\frac{1}{2} \cdot \log\left(\frac{1}{2}\right) + \frac{1}{2} \cdot \log\left(\frac{1}{2}\right)\right) \\ & E_2 = E(\text{WHW} \geq 36) = E(9 \text{ B}, 5 \text{ G}) = -\left(\frac{9}{14} \cdot \log\left(\frac{9}{14}\right) + \frac{5}{14} \cdot \log\left(\frac{5}{14}\right)\right) \end{align*} $$

>[!Exercice  à faire]
1- Calculer d abord en tenant de l'hypothèse
2- calculer en tenant compte de l hypothèse de l'arbre binaire

