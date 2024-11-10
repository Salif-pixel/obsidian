
---

#  Classe Cercle
## Définition

#### Copie Profonde :
une copie profonde crée une copie complète de l'objet , y compris de tous les objets internes donc chaque objet  de la hiérarchie est réplique de sorte que les instances copiées sont indépendantes.


#### Copie Superficielle :
une copie superficielle crée un nouvel objet mais ne copie pas en profondeur  les objets internes il copie juste les références de ces objets , ces objets internes ne sont donc pas dupliqués.



>[!Classe Cercle]
```java
public class Cercle {  
    private int rayon;  
    private Point centre;  
    public Cercle (int rayon, Point centre) {  
        this.rayon = rayon;  
        this.centre = centre;  
    }  
    public int getRayon() {  
        return rayon;  
    }  
    public Point getCentre() {  
        return centre;  
    }  
    public void setCentre(Point centre) {  
        this.centre = centre;  
    }  
    public void setRayon(int rayon) {  
        this.rayon = rayon;  
    }  
}
```

>[!Classe Point]
```java
public class Point {  
    private int x;  
    private int y;  
    public Point(int x, int y) {  
        this.x = x;  
        this.y = y;  
    }  
    public int getX() {  
        return x;  
    }  
    public int getY() {  
        return y;  
    }  
    public void setX(int x) {  
        this.x = x;  
    }  
    public void setY(int y) {  
        this.y = y;  
    }  
  
}
```

>[!Classe Main]
```java
public class Main {  
    public static void main(String[] args) {  
        Point centre = new Point(100, 100);  
        
        Cercle original= new Cercle(2,centre);  
        
        Cercle copiesuperficielle = new Cercle(original.getRayon(),original.getCentre());  
        
        Cercle copieprofonde= new Cercle(original.getRayon(),new Point(centre.getX(),centre.getY()));  
        
        System.out.println("original "+original.getCentre().getX());   //100
        
        System.out.println("copieprofonde "+copieprofonde.getCentre().getX());   //100
        
        System.out.println("copiesuperficielle "+copiesuperficielle.getCentre().getX());  //100
    }  
}
```

## Cas Copie superficielle
```java
public class Main {  
    public static void main(String[] args) {  
        Point centre = new Point(100, 100);  
        
        Cercle original= new Cercle(2,centre);  
        
        Cercle copiesuperficielle = new Cercle(original.getRayon(),original.getCentre());  
    
        Cercle copieprofonde= new Cercle(original.getRayon(),new Point(centre.getX(),centre.getY()));
        
        copiesuperficielle.getCentre().setX(200);  
        
        System.out.println("original "+original.getCentre().getX());   //200
        
        System.out.println("copieprofonde "+copieprofonde.getCentre().getX());   //100
        
        System.out.println("copiesuperficielle "+copiesuperficielle.getCentre().getX());  //200
    }  
}
```

on remarque qu'ici étant donne que la copie superficielle et l'orignal référence le même objet Centre donc si il y'a une quelconque modification sur cette objet centre de type point alors tous les deux verront cette modification

## Cas Copie profonde
```java
public class Main {  
    public static void main(String[] args) {  
        Point centre = new Point(100, 100);  
        
        Cercle original= new Cercle(2,centre);  
        
        Cercle copiesuperficielle = new Cercle(original.getRayon(),original.getCentre());  
        
        Cercle copieprofonde= new Cercle(original.getRayon(),new Point(centre.getX(),centre.getY
		   
        copieprofonde.getCentre().setX(200);  
        
        System.out.println("original "+original.getCentre().getX());   //100
        
        System.out.println("copieprofonde "+copieprofonde.getCentre().getX());   //200
        
        System.out.println("copiesuperficielle "+copiesuperficielle.getCentre().getX());  //100
    }  
}

```

on remarque qu'ici étant donne que la copie profonde copie carrément l'orignal l'objet interne centre est diffèrent pour chacun d'eux , donc les deux objets étant indépendant si l'ont modifie l'un cela n'impactera pas l'autre

---

#  Classe Fraction
## Introduction

La classe `Fraction` est conçue pour représenter et manipuler des fractions arithmétiques. Elle offre diverses méthodes pour effectuer des opérations fondamentales telles que l'addition, la soustraction, la multiplication et la division de fractions la division d'une fraction et l'inversion d'une fraction . De plus, elle gère des cas particuliers comme la division par zéro en utilisant une exception personnalisée `DivisionParZeroException`.

## Structure de la Classe

### Attributs

- `numerator`  : Le numérateur de la fraction.
- `denominator` : Le dénominateur de la fraction.

### Constructeur

- **`Fraction(int numerator, int denominator)`** : Initialise une fraction avec un numérateur et un dénominateur. Lève une exception si le dénominateur est égal à zéro.

```java
public class Fraction {  
    private int numerator;  
    private int denominator;  
  
    public Fraction(int numerator, int denominator) throws DivisionParZeroException {  
        this.numerator = numerator;  
        if(denominator == 0) 
        throw new DivisionParZeroException("Attention le denominateur doit être différent de 0 ");  
        this.denominator = denominator;  
    }
```
### Méthodes

1. **Getters et Setters** :

- `getNumerator()`: Retourne le numérateur.
- `setNumerator(int numerator)`: Modifie le numérateur.
- `getDenominator()`: Retourne le dénominateur.
- `setDenominator(int denominator)`: Modifie le dénominateur avec validation pour éviter la division par zéro.

```java
public int getNumerator() {  
 return numerator;  
}  
public void setNumerator(int numerator) {  
  this.numerator = numerator;  
}  
public int getDenominator() {  
  return denominator;  
}  
public void setDenominator(int denominator) throws DivisionParZeroException {  
  if(denominator == 0) 
  throw new DivisionParZeroException("Attention le denominateur doit être différent de 0 ");  
  this.denominator = denominator;  
}

```

1. **Opérations sur les Fractions** :

- `Division()`: Calcule et retourne la valeur décimale de la fraction.

```java 
public  double Division() {  
   return (double) numerator / denominator;  
}
```

- `InverserFraction()`: Inverse les valeurs de numérateur et de dénominateur. Lève une exception si le numérateur est zéro.

```java
public  void InverserFraction() throws DivisionParZeroException {  
   if(numerator == 0) 
   throw new DivisionParZeroException("Attention le denominateur doit être différent de 0  ");  
   int temp =numerator;  
   numerator = denominator;  
   denominator=temp;  
}
```

- `afficherFraction( Fraction f1 )`: Affiche la fraction sous forme de chaîne.

```java
public static void afficherFraction( Fraction f1 ){  
    System.out.printf("voici la fraction  %d/%d = %.2f\n", f1.getNumerator(),
    f1.getDenominator(),f1.Division());    
}
```

- `additionFraction(Fraction f1, Fraction f2)`: Additionne deux fractions et affiche le résultat.

```java
public static Fraction additionFraction(Fraction f1, Fraction f2) throws DivisionParZeroException {  
    int numresultat = f1.getNumerator() * f2.getDenominator() + f2.getNumerator() * f1.getDenominator();  
    int denominator = f1.getDenominator() * f2.getDenominator();  
    int pgcd= PGCD(numresultat, denominator);  
    numresultat = numresultat/=pgcd;  
    denominator = denominator/=pgcd;  
    Fraction f = new Fraction(numresultat,denominator);  
    return f;  
}
```

- `soustraireFraction(Fraction f1, Fraction f2)`: Soustrait la seconde fraction de la première et affiche le résultat.

```java
public static Fraction soustraireFraction(Fraction f1, Fraction f2) throws DivisionParZeroException {  
    int numresultat = f1.getNumerator() * f2.getDenominator() - f2.getNumerator() * f1.getDenominator();  
    int denominator = f1.getDenominator() * f2.getDenominator();  
    int pgcd= PGCD(numresultat, denominator);  
    numresultat = numresultat/=pgcd;  
    denominator = denominator/=pgcd;  
    Fraction f = new Fraction(numresultat,denominator);  
    return f;  
}
```

- `diviserFraction(Fraction f1, Fraction f2)`: Divise la première fraction par la seconde et affiche le résultat.

```java
public static Fraction diviserFraction(Fraction f1, Fraction f2) throws DivisionParZeroException   {  
    if(f2.getNumerator()==0) 
    throw new 
    DivisionParZeroException("Attention le numerateur de la deuxieme fraction doit être différent de 0 ");  
    int numresultat = f1.getNumerator() * f2.getDenominator() ;  
    int denominator = f2.getNumerator() * f1.getDenominator();  
    int pgcd= PGCD(numresultat, denominator);  
    numresultat = numresultat/=pgcd;  
    denominator = denominator/=pgcd;  
    Fraction f = new Fraction(numresultat,denominator);  
    return f;  
}
```

- `multiplierFraction(Fraction f1, Fraction f2)`: Multiplie deux fractions et affiche le résultat.

```java
public static Fraction multiplierFraction(Fraction f1, Fraction f2) throws DivisionParZeroException {  
    int numresultat = f1.getNumerator() * f2.getNumerator() ;  
    int denominator = f2.getDenominator() * f1.getDenominator();  
    int pgcd= PGCD(numresultat, denominator);  
    numresultat = numresultat/=pgcd;  
    denominator = denominator/=pgcd;  
    Fraction f = new Fraction(numresultat,denominator);  
    return f;  
}
```

- `PGCD(int a, int b)`: Méthode privée pour calculer le Plus Grand Commun Diviseur, utilisée pour simplifier les résultats.

 ```java
private static int PGCD(int a, int b){  
   if(b == 0) return a;  
   else return PGCD(b, a % b);  
}
```

### Exception

- `DivisionParZeroException`: Classe d'exception appelé au cas ou un dénominateur n'est pas différent de 0

```java
public class DivisionParZeroException extends Exception{  
    public DivisionParZeroException(String msg){  
        super(msg);  
    }  
}
```

## Objectifs des Tests

L’objectif principal est de vérifier que les méthodes de la classe `Fraction` produisent les résultats attendus pour chaque opération. Plus précisément, nous évaluons les méthodes suivantes :

- `multiplierFraction`
- `additionFraction`
- `soustraireFraction`
- `diviserFraction`
- `InverserFraction`
- `afficherFraction`
- `Division` (ou la méthode pour obtenir la valeur décimale de la fraction)

## Plan de Tests

Les tests consistent en :

1. **Création des fractions** : Initialisation de fractions avec différents numérateurs et dénominateurs.
2. **Opérations de base** : Multiplication, addition, soustraction, division entre deux fractions.
3. **Inversion de fraction** : Inversion du numérateur et du dénominateur de chaque fraction.
4. **Affichage** : Affichage de la fraction sous forme "numérateur/dénominateur".
5. **Division décimale** : Vérification de la valeur décimale des fractions.

## Résultats des Tests

### 1. Multiplication (`multiplierFraction`)

```java
public class Main {  
    public static void main(String[] args)  {  
        try {  
           Fraction f1 = new Fraction(4, 2);  
           Fraction f2 = new Fraction(1, 2);  
           Fraction.afficherFraction(Fraction.multiplierFraction(f1,f2));
           // sortie terminal: voici la fraction  1/1 = 1,00
        }catch (DivisionParZeroException exception){  
            System.out.println(exception.getMessage());  
        }  
          }  
}
```

 **Test** : `Fraction result = Fraction.multiplierFraction(f1, f2);`
- **Objectif** : Vérifier que la multiplication est correcte.
- **Résultat Attendu** : `result` devrait avoir un numérateur de `4` et un dénominateur de `4` (ou être simplifié en `1/1`).
- **Résultat Obtenu** : La fraction simplifiée obtenue est `1/1`. Test validé.

### 2. Addition (`additionFraction`)
```java
public class Main {  
    public static void main(String[] args)  {  
        try {  
           Fraction f1 = new Fraction(4, 2);  
           Fraction f2 = new Fraction(1, 2);  
           Fraction.afficherFraction(Fraction.additionFraction(f1,f2));
           // sortie terminal: voici la fraction  5/2 = 2,50
        }catch (DivisionParZeroException exception){  
            System.out.println(exception.getMessage());  
        }  
          }  
}
```

- **Test** : `Fraction result = Fraction.additionFraction(f1, f2);`
- **Objectif** : Additionner les fractions et obtenir le résultat correct.
- **Résultat Attendu** : `result` devrait être `5/2` .
- **Résultat Obtenu** : La fraction simplifiée est `5/2`. Test validé.

### 3. Soustraction (`soustraireFraction`)
```java
public class Main {  
    public static void main(String[] args)  {  
        try {  
           Fraction f1 = new Fraction(4, 2);  
           Fraction f2 = new Fraction(1, 2);  
           Fraction.afficherFraction(Fraction.soustraireFraction(f1,f2));
           // sortie terminal: voici la fraction  3/2 = 1,50
        }catch (DivisionParZeroException exception){  
            System.out.println(exception.getMessage());  
        }  
          }  
}
```

- **Test** : `Fraction result = Fraction.soustraireFraction(f1, f2);`
- **Objectif** : Vérifier que la soustraction est correcte.
- **Résultat Attendu** : `result` devrait être `3/2`.
- **Résultat Obtenu** : La fraction simplifiée est `3/2`. Test validé.

### 4. Division (`diviserFraction`)
```java
public class Main {  
    public static void main(String[] args)  {  
        try {  
           Fraction f1 = new Fraction(4, 2);  
           Fraction f2 = new Fraction(1, 2);  
           Fraction.afficherFraction(Fraction.diviserFraction(f1,f2));
           // sortie terminal: voici la fraction  4/1 = 4,00 
        }catch (DivisionParZeroException exception){  
            System.out.println(exception.getMessage());  
        }  
          }  
}
```

- **Test** : `Fraction result = Fraction.diviserFraction(f1, f2);`
- **Objectif** : Vérifier que la division produit le résultat correct.
- **Résultat Attendu** : `result` devrait être `4/1`.
- **Résultat Obtenu** : `4/1`. Test validé.

### 5. Inversion (`InverserFraction`)

```java
public class Main {  
    public static void main(String[] args)  {  
        try {  
           Fraction f1 = new Fraction(4, 2);  
           Fraction f2 = new Fraction(1, 2);  
           f1.InverserFraction();  
		   f2.InverserFraction();  
		   Fraction.afficherFraction(f1.getNumerator(),f1.getDenominator());//voici la fraction  2/4 =0,50
		   Fraction.afficherFraction(f2.getNumerator(),f2.getDenominator());//voici la fraction  2/1 =2,00
        }catch (DivisionParZeroException exception){  
            System.out.println(exception.getMessage());  
        }  
          }  
}
```

- **Test** : `f1.InverserFraction(); f2.InverserFraction();`
- **Objectif** : Vérifier que les fractions sont correctement inversées.
- **Résultat Attendu** : `f1` devrait être `2/4`, et `f2` devrait être `2/1` après inversion.
- **Résultat Obtenu** : Les fractions sont correctement inversées. Test validé.

### 6. Affichage (`afficherFraction`)
```java
public class Main {  
    public static void main(String[] args)  {  
        try {  
           Fraction f1 = new Fraction(4, 2);  
           Fraction f2 = new Fraction(1, 2);  
		   Fraction.afficherFraction(f1.getNumerator(),f1.getDenominator());//voici la fraction  2/1 =2,00
		   Fraction.afficherFraction(f2.getNumerator(),f2.getDenominator());//voici la fraction  1/2 =0,50
        }catch (DivisionParZeroException exception){  
            System.out.println(exception.getMessage());  
        }  
          }  
}
```

- **Test** : `Fraction.afficherFraction(f1.getNumerator(), f1.getDenominator());`
- **Objectif** : Vérifier que l'affichage est sous forme correcte (`numérateur/dénominateur`).
- **Résultat Attendu** : `f1` devrait être `2/1`, et `f2` devrait être `1/2` .
- **Résultat Obtenu** : Conforme aux attentes. Test validé.

### 7. Division Décimale (`Division`)
```java
public class Main {  
    public static void main(String[] args)  {  
        try {  
           Fraction f1 = new Fraction(4, 2);  
           Fraction f2 = new Fraction(1, 2);  
		   System.out.println(f1.Division());  // 2.0
		   System.out.println(f2.Division());  //0.5
        }catch (DivisionParZeroException exception){  
            System.out.println(exception.getMessage());  
        }  
          }  
}
```

- **Test** : `System.out.println(f1.Division());`
- **Objectif** : Obtenir la valeur décimale de `f1`.
- **Résultat Attendu** : `f1` devrait donner `0.5`.
- **Résultat Obtenu** : Résultat correct. Test validé.\

### 7. Dénominateur= 0 (`DivisionParZeroException`)
```java
public class Main {  
    public static void main(String[] args)  {  
        try {  
           Fraction f1 = new Fraction(4, 0);  
		   Fraction f2 = new Fraction(1, 2););  
		   System.out.println(f1.Division());  
		   System.out.println(f2.Division());  
        }catch (DivisionParZeroException exception){  
            System.out.println(exception.getMessage());// Attention le denominateur doit être différent de 0 

        }  
          }  
}
```

- **Test** : `Fraction f1 = new Fraction(4, 0);`
- **Objectif** : initialiser  `f1`.
- **Résultat Attendu** : Erreur car un dénominateur ne doit pas être égal a 0.
- **Résultat Obtenu** : Résultat correct. Test validé.
## Conclusion

Les tests confirment que les méthodes de la classe `Fraction` fonctionnent conformément aux attentes pour les opérations de base, l’inversion, l'affichage  etc. Aucune erreur n’a été rencontrée, ce qui valide l’implémentation actuelle de la classe.

---
