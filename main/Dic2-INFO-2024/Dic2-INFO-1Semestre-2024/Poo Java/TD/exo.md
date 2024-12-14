
---
##  la classe A est correcte 

### Définition des méthodes
- **f(int n, float x)**  
- **f(float x1, float x2)**  
- **f(float x, int n)**  

## Cas d'utilisation

### 1. Appel : `a.f(n1.x)`  
- Méthode appelée : **f(int n, float x)**  
- Justification : Correspondance directe avec les paramètres fournis.

### 2. Appel : `a.f(x, n1)`  
- Méthode appelée : **f(float x, int n)**  
- Justification : Correspondance directe avec les paramètres fournis.

### 3. Appel : `a.f(p, x)`  
- Méthode appelée : **f(int n, float x)**  
- Justification : Conversion implicite de `p` en `int` 

