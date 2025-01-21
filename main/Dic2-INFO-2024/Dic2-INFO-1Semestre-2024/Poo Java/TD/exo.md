
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

### 4. Appel : `a.f(n1, n2)`  
on aura un problème de choix entre la première et la dernière méthode


### **Est-ce que la classe A est correcte ?**

Oui, **la classe A est correcte** en termes de syntaxe, car en Java, la surcharge de méthode est autorisée tant que les signatures des fonctions sont différentes. 

Dans cette classe :

1. `f(int n, float x)`
2. `f(float x1, float x2)`
3. `f(float x, int n)`

Les trois méthodes sont correctement différenciées par les types et l'ordre des paramètres. Cela respecte les règles de **surcharge**.

---

### **Quelles instructions sont correctes et quelles méthodes sont appelées ?**

1. **`a.f(n1, x);`**
    
    - `n1` est un `int` et `x` est un `float`.
    - Cela correspond directement à `f(int, float)`.  
        **Méthode appelée :  `f(int n, float x)`**
2. **`a.f(x, n1);`**
    
    - `x` est un `float` et `n1` est un `int`.
    - Cela correspond directement à `f(float x, int n)`.  
        **Méthode appelée : `f(float x, int n)`**
3. **`a.f(p, x);`**
    
    - `p` est un `short` et `x` est un `float`.
    - Un `short` peut être converti implicitement en `int` .
    - Cela correspond à `f(int n, float x)` après la conversion de `short` en `int`.  
        **Méthode appelée : `f(int n, float x)` avec conversion implicite de `short` en `int`.**
4. **`a.f(n1, n2);`**
    
    - `n1` et `n2` sont des `int`.
    - Aucune méthode ne correspond exactement à la signature `f(int, int)`.
    - on aura donc 3 possibilités
    -  `f(int n, float x)`
	-  `f(float x1, float x2)`
	-  `f(float x, int n)`
	- la deuxième ne sera pas choisit car les deux autre requiert moins de conversion 
    - Le compilateur génère une erreur d'ambiguïté, car il ne trouve pas de correspondance unique.