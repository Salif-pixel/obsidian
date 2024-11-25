
---


## Introduction
Dans cet exercice, l'objectif était de créer une classe `Table` permettant de gérer une table de taille maximale fixe, d'y ajouter des éléments et de parcourir ces derniers à l'aide d'un itérateur. L'exercice explore les concepts de classes internes, locales, et externes, ainsi que leur interaction avec des interfaces telles que `Iterator`.

---

## Description de la classe `Table`

La classe `Table` représente une structure de données capable de contenir un tableau d'entiers avec une taille maximale spécifiée lors de la construction. Voici les détails :

## Code de la classe `Table` avec la `classe locale`
l'itérateur a été défini comme une classe locale au sein de la méthode `Iterator` :

```java
import java.util.Iterator;
import java.util.NoSuchElementException;

public class Table {
    int[] elements;
    private int tailleMax;
    private int currentsize;

    public Table(int tailleMax) {
        this.tailleMax = tailleMax;
        this.elements = new int[tailleMax];
    }

    public void add(int element) {
        if (currentsize == tailleMax) {
            System.out.println("Taille max atteinte");
        } else {
            elements[currentsize] = element;
            currentsize++;
        }
    }

    public int size() {
        return currentsize;
    }

    public Iterator<Object> iterator() {
        // Classe locale
        class TableIterator implements Iterator<Object> {
            private int index;

            @Override
            public boolean hasNext() {
                return index < size();
            }

            @Override
            public Object next() {
                if (!hasNext()) throw new NoSuchElementException();
                return elements[index++];
            }

            @Override
            public void remove() {
                throw new UnsupportedOperationException();
            }
        }
        return new TableIterator();
    }
}
```

---

##  Code de la classe `Table` avec la `classe interne TableIterator`

l'itérateur a été défini comme une classe interne au sein de `Table` :

```java
import java.util.ArrayList;  
import java.util.Iterator;  
import java.util.List;  
import java.util.NoSuchElementException;  
  
  
public class Table {  
    int [] elements;  
    private int tailleMax;  
    private int currentsize;  
    public Table(int tailleMax){  
        this.tailleMax = tailleMax;  
        this.elements = new int[tailleMax];  
    }  
    public void add(int element){  
        if(currentsize == tailleMax){  
            System.out.println("Taille max ");  
        }else{  
            elements[currentsize] = element;  
            currentsize++;  
        }  
  
    }  
    public int size(){  
        return currentsize;  
    }  
    public Iterator<Object> iterator(){  
        return new TableIterator();  
    } 
      // Classe interne
    private class TableIterator implements Iterator<Object> {  
        private int index ;  
  
        @Override  
        public boolean hasNext() {  
            return index< size();  
        }  
  
        @Override  
        public Object next() {  
            if(!hasNext()) throw new NoSuchElementException();  
            return elements[index++];  
        }  
        @Override  
        public void remove() {  
            throw new UnsupportedOperationException();  
        }  
    }  
}
```

---

##  Code de la classe `Table` avec la `Classe externe TableIterator`

La classe `TableIterator` a ensuite été déplacée dans un fichier séparé pour en faire une classe externe. Cela permet une meilleure réutilisabilité et séparation des responsabilités.

### Code de la classe externe

#### Classe `Table`
```java
import java.util.ArrayList;  
import java.util.Iterator;  
import java.util.List;  
import java.util.NoSuchElementException;  
  
  
public class Table {  
    int [] elements;  
    private int tailleMax;  
    private int currentsize;  
    public Table(int tailleMax){  
        this.tailleMax = tailleMax;  
        this.elements = new int[tailleMax];  
    }  
    public void add(int element){  
        if(currentsize == tailleMax){  
            System.out.println("Taille max ");  
        }else{  
            elements[currentsize] = element;  
            currentsize++;  
        }  
  
    }  
    public int size(){  
        return currentsize;  
    }  
    public Iterator<Object> iterator(){  
        return new TableIterator(this);  
    }  
    
}
```

#### Classe `TableIterator`

```java
import java.util.Iterator;
import java.util.NoSuchElementException;

public class TableIterator implements Iterator<Object> {
    private int index;
    private final Table table;

    public TableIterator(Table table) {
        this.table = table;
    }

    @Override
    public boolean hasNext() {
        return index < table.size();
    }

    @Override
    public Object next() {
        if (!hasNext()) throw new NoSuchElementException();
        return table.elements[index++];
    }

    @Override
    public void remove() {
        throw new UnsupportedOperationException();
    }
}
```

---

## Comparaison des implémentations

| **Critère**               | **Classe interne**                      | **Classe locale**                 | **Classe externe**                     |
| ------------------------- | --------------------------------------- | --------------------------------- | -------------------------------------- |
| **Portée**                | Accessible dans toute la classe `Table` | Limitée à la méthode `iterator()` | Séparée, accessible à d'autres classes |


---
## Main
```java
import java.util.Iterator;  
  
public class Main {  
    public static void main(String[] args) {  
        Table table = new Table(5);  
        table.add(1);  
        table.add(2);  
        System.out.println("voici la taille de la table "+ table.size());  
        Iterator<Object> iterator = table.iterator();  
        while (iterator.hasNext()) {  
            System.out.println(iterator.next());  
        }  
    }  
}
	 //voici la taille de la table 2
	// 1
   //  2
```