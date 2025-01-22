
---



Ce tutoriel vous guide à travers les étapes de création, d'organisation, de compilation et d'archivage de projets Java, ainsi que l'exécution de fichiers JAR. Nous utiliserons deux projets : **Projet1** et **Projet2**.

---

## 🌐 Structure des Dossiers

Commencez par créer l'arborescence suivante :

```bash
TpJava
├── Projet1
│   ├── archives
│   ├── bin
│   ├── doc
│   └── src
│       └── Fraction.java
└── Projet2
    ├── archives
    ├── bin
    ├── doc
    └── src
        └── TesterFraction.java
```

---

## 🔧 Implémentation des Fichiers Java

### Fichier `Fraction.java` (Projet1/src)

Ajoutez le code suivant dans `Fraction.java` :

```java
// Définition du package
package fr.upmc.master;

// Classe de gestion de fractions
/**
 * Code de la classe de gestion de Fractions
 */
public class Fraction {
    // Champs : numérateur et dénominateur
    int num;
    int den;

    /**
     * Constructeur de la classe
     * @param n le numérateur
     * @param d le dénominateur
     */
    public Fraction(int n, int d) {
        num = n;
        den = d;
    }

    /**
     * Méthode pour inverser la fraction
     * @return une nouvelle fraction inversée
     */
    public Fraction inverser() {
        if (this.num != 0) return new Fraction(this.den, this.num);
        else return null;
    }

    /**
     * Méthode pour afficher la fraction
     */
    public void afficher() {
        if (this.num % this.den == 0) {
            System.out.println(this.num / this.den);
        } else {
            System.out.println(this.num + "/" + this.den);
        }
    }
}
```

### Fichier `TesterFraction.java` (Projet2/src)

Ajoutez le code suivant dans `TesterFraction.java` :

```java
// Définition du package
package sn.esp.dgi.dic;
import fr.upmc.master.Fraction;

// Classe principale pour tester Fraction
public class TesterFraction {
    public static void main(String[] args) {
        Fraction f1 = new Fraction(5, 3);
        f1.afficher();
    }
}
```

---

## 🔧 Compilation et Organisation des Fichiers

### Compilation de `Fraction.java` (Projet1)

1. Placez-vous dans le répertoire **Projet1** :
    
    ```bash
    cd Projet1
    ```
    
2. Compilez `Fraction.java` et placez les fichiers compilés dans `bin` :
    
    ```bash
    javac -d "./bin" src/Fraction.java
    ```
    
3. Vérifiez l'arborescence :
    
    ```bash
    tree
    ```
    
    Vous devriez obtenir :
    
    ```bash
    .
    ├── archives
    ├── bin
    │   └── fr
    │       └── upmc
    │           └── master
    │               └── Fraction.class
    ├── doc
    └── src
        └── Fraction.java
    ```
    

### Compilation de `TesterFraction.java` (Projet2)

1. Compilez `TesterFraction.java` en spécifiant le chemin des classes compilées de Projet1 :
    
    ```bash
    javac -d "../Projet2/bin" -cp "./bin" ../Projet2/src/TesterFraction.java
    ```
    
2. Vérifiez l'arborescence :
    
    ```bash
    tree
    ```
    
    Vous devriez obtenir :
    
    ```bash
    .
    ├── Projet2
    │   ├── archives
    │   ├── bin
    │   │   └── sn
    │   │       └── esp
    │   │           └── dgi
    │   │               └── dic
    │   │                   └── TesterFraction.class
    │   ├── doc
    │   └── src
    │       └── TesterFraction.java
    ```
    

---

## 🔨 Exécution des Programmes

Exécutez `TesterFraction` :

```bash
java -cp "../Projet2/bin:./bin" sn.esp.dgi.dic.TesterFraction
```

Vous devriez voir :

```plaintext
5/3
```

---

## 🔧 Création de Fichiers JAR

### Archivage du Projet1

1. Placez-vous dans le répertoire `bin` de **Projet1** :
    
    ```bash
    cd bin
    ```
    
2. Créez un fichier JAR :
    
    ```bash
    jar cf ../archives/projet1.jar .
    ```
    
3. Vérifiez l'arborescence :
    
    ```bash
    tree
    ```
    
    Vous devriez obtenir :
    
    ```bash
    ├── archives
    │   └── projet1.jar
    ├── bin
    │   └── fr
    │       └── upmc
    │           └── master
    │               └── Fraction.class
    └── src
        └── Fraction.java
    ```
    
4. Exécutez avec le fichier JAR :
    
    ```bash
    java -cp "../Projet2/bin:./archives/projet1.jar"   sn.esp.dgi.dic.TesterFraction
    ```
    
    Vous obtiendrez :
    
    ```plaintext
    5/3
    ```
    

### Archivage du Projet2

1. Placez-vous dans le répertoire `bin` de **Projet2** :
    
    ```bash
    cd ../Projet2/bin
    ```
    
2. Créez un fichier JAR :
    
    ```bash
    jar cf ../archives/projet2.jar .
    ```
    
3. Exécutez avec les fichiers JAR :
    
    ```bash
    java -cp "../Projet2/archives/projet2.jar:./archives/projet1.jar" sn.esp.dgi.dic.TesterFraction
    ```
    
    Vous obtiendrez :
    
    ```plaintext
    5/3
    ```
    

---

## 🔧 Extraction des Fichiers JAR

Pour extraire le contenu d'un fichier JAR :

1. Exécutez :
    
    ```bash
    jar xf ./archives/projet1.jar
    ```
    
2. Vérifiez l'arborescence :
    
    ```bash
    tree
    ```
    
    Vous verrez le contenu extrait, y compris le répertoire `META-INF` et les classes.
    

---
