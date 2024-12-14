
---
# I. Notation
# II. Polynôme de Lagrange
# II. Polynôme d'interpolation de Newton
## 1. Forme explicite du polynôme de Newton
## 2. Différence divisée

### => Les différences divisées d'ordre 1 sont définies par:

$$F[x_i,x_{i+1}]=\frac{f(x_{i+1})-f(x_i)}{x_{i+1}-x_i}$$
### =>Les différences divisées d'ordre 2 sont définies par:

$$F[x_i,x_{i+1},x_{i+2}]=\frac{F[x_{i+1},x_{i+2}]-F[x_{i},x_{i+1}]}{x_{i+2}-x_i}$$
### => Les différences divisées d'ordre n sont définies a partir des différences divisées d'ordre (n-1)
$$F[x_i,x_{i+1},x_{i+2},...x_{i+n}]=\frac{F[x_{i+1},....,x_{i+n}]-F[x_{i},x_{i+1},....,x_{i+(n-1)}]}{x_{i+n}-x_i}$$
### => Table des différences divisées


| $$x_i$$ | $$f(xi)f(x_i)$$ | $$F[xi,xi+1]F[x_i, x_{i+1}]$$ | $$F[xi,xi+1,xi+2]F[x_i, x_{i+1}, x_{i+2}]$$ | $$F[xi,…,xi+n]F[x_i, \dots, x_{i+n}]$$ |
| ------- | --------------- | ----------------------------- | ------------------------------------------- | -------------------------------------- |
| $$x_0$$ | $$f(x_0)$$      |                               |                                             |                                        |
| $$x_1$$ | $$f(x_1)$$      | $$F[x0,x1]$$                  |                                             |                                        |
| $$x_2$$ | $$f(x_2)$$      | $$F[x1,x2]$$                  | $$F[x0,x1,x2]F[x_0, x_1, x_2]$$             |                                        |
| $$x_n$$ | $$f(x_n)$$      |                               |                                             | $$F[x0,…,xn]F[x_0, \dots, x_n]$$       |

