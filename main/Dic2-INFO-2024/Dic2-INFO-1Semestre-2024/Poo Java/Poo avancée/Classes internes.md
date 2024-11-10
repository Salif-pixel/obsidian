
---
# Classes internes
>[!Analyse des besoins]
>
>L'objectif de l'analyse est de comprendre les besoins de l'application et d'identifier les principales fonctionnalités. Cette phase comprend généralement :

- **Identification des besoins** : Comprendre ce que le logiciel doit accomplir, généralement en consultant les utilisateurs ou les parties prenantes.
- **Définition des cas d'utilisation** : Décrire les interactions principales entre l'utilisateur et le système sous forme de **cas d'utilisation**, qui illustrent les fonctionnalités attendues.
- **Diagrammes UML** : On utilise souvent des diagrammes de classes pour représenter les objets et leurs relations, ainsi que des diagrammes de cas d’utilisation pour illustrer les interactions.

>[!Conception de la solution]
>La **conception** en développement logiciel, c'est le processus de planification et d'organisation du code pour qu'il soit clair, efficace et facile à maintenir. Elle consiste à définir comment les différentes parties de l'application vont fonctionner ensemble, avant même de commencer à coder. C'est l'activité a travers la quelle on indique comment le système doit être réalisé

- **Définition des classes et des objets** : On décompose le modèle de domaine en **classes** et on définit leurs attributs, méthodes, et relations. Cela inclut aussi l’application des principes SOLID pour une bonne organisation.
- **Définition de l'architecture** : Elle définie la structure du logicielle en terme d'entité et leur interaction relation etc. 
	Choisir une architecture (par exemple, MVC) pour structurer le code de manière modulaire et réutilisable.
- **Diagrammes UML de conception** : Utiliser des diagrammes de séquence, de composants, de classes de conception et d’autres types de diagrammes UML pour planifier l'interaction entre objets, le flux de données et les interactions avec l'utilisateur.
- **Conception des interfaces** : Définir des interfaces qui facilitent la réutilisabilité et l'extensibilité du code
- **Choix des outils et technologies choisies**

`Comment aider le concepteur a prendre en charge certaines difficultés?`

## Définition:
une classe interne est une classe dont la définition se situe dans une autre classe,
un objet de classe interne est toujours relié a un objet englobant de classe externe
L'objet englobant peut voir les parties privées de l'objet englobé
et de même dans l'autre sens l'objet englobé peut voir les parties privées de l'objet englobant
#### Exemple: Objet englobant et englobé
```java
public class E { // Classe externe
    private int x = 10;
    static int y = 20;

    public int addition() {
    
        return (x + y);
    }

    public class I { // Classe interne
        final int k = 12;

        public int multiplier() {
            return x * y;
        }
    }

    public static void main(String[] args) {
        E e = new E();    //e est l'objet englobant
        I i = e.new I(); //i est l'objet englobé
        System.out.println(i.multiplier());
    }
}
```

#### Example2: Objet englobant et englobé implicite
```java
public class E { // Classe externe
    private int x = 10;
    static int y = 20;

    public int addition() {
	     I i = new I(); 
        return (x + y);
    }

    public class I { // Classe interne
        final int k = 12;

        public int multiplier() {
            return x * y;
        }
    }

    public static void main(String[] args) {
        E e = new E();    //e est l'objet englobant
        System.out.println(e.addition()); // l'instance i de la methode addition devient l'objet englobé
    }
}
```

#### Example3: Objet englobant et englobé cas méthode addition static
```java
public class E { // Classe externe
    private int x = 10;
    static int y = 20;

    public static int addition() {
	     E e = new E();  //e est l'objet englobant
	     I i = new I(); //i est l'objet englobé
        return (x + y);
    }

    public class I { // Classe interne
        final int k = 12;

        public int multiplier() {
            return x * y;
        }
    }

    public static void main(String[] args) {
        System.out.println(E.addition()); 
    }
}
```