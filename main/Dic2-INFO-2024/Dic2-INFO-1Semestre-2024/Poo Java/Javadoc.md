# Cours Javadoc

## Qu'est-ce que Javadoc ?
Javadoc est un outil fourni avec le JDK (Java Development Kit) qui permet de générer une documentation au format HTML à partir des commentaires de code Java.  
C'est essentiel pour rendre votre code compréhensible et maintenable.

## Syntaxe de base des commentaires Javadoc
Les commentaires Javadoc commencent par `/**` et se terminent par `*/`. Ils doivent être placés juste avant les classes, méthodes ou champs que vous souhaitez documenter.

### Exemple :
```java
/**
 * Cette classe représente une personne.
 * Elle contient les informations de base comme le nom et l'âge.
 */
public class Person {
    private String name;
    private int age;

    /**
     * Constructeur pour initialiser une personne.
     * 
     * @param name Le nom de la personne.
     * @param age L'âge de la personne.
     */
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    /**
     * Obtenir le nom de la personne.
     * 
     * @return Le nom de la personne.
     */
    public String getName() {
        return name;
    }

    /**
     * Modifier le nom de la personne.
     * 
     * @param name Le nouveau nom.
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * Obtenir l'âge de la personne.
     * 
     * @return L'âge de la personne.
     */
    public int getAge() {
        return age;
    }

    /**
     * Modifier l'âge de la personne.
     * 
     * @param age Le nouvel âge.
     */
    public void setAge(int age) {
        this.age = age;
    }
}
````

## Les balises Javadoc courantes
Voici quelques balises utiles que vous pouvez utiliser dans vos commentaires Javadoc :

- `@param` : Décrit un paramètre d'une méthode ou d'un constructeur.
- `@return` : Décrit la valeur de retour d'une méthode.
- `@throws` ou `@exception` : Documente les exceptions levées par une méthode.
- `@author` : Indique l'auteur du code.
- `@version` : Indique la version de la classe ou de la méthode.
- `@see` : Référence d'autres éléments (classes, méthodes, etc.).
- `@since` : Indique la version à partir de laquelle un élément est disponible.
## La commande `javadoc`
La commande `javadoc` est utilisée pour générer automatiquement de la documentation au format HTML à partir de commentaires Javadoc dans vos fichiers Java.  
### Syntaxe de base
```bash
javadoc [options] [fichiers_source]
````

### Options principales de la commande
Voici les options les plus courantes pour utiliser efficacement la commande `javadoc` :

- `-d` : Spécifie le dossier où la documentation générée sera placée.  
    **Exemple :**
    
    ```bash
    javadoc -d ./doc Person.java
    ```
    
- `-sourcepath` : Définit le chemin vers les fichiers source à documenter.  
    **Exemple :**
    
    ```bash
    javadoc -sourcepath ./src -d ./doc Person.java
    ```
    
- `-classpath` : Ajoute le chemin des bibliothèques nécessaires au traitement du fichier source.  
    **Exemple :**
    
    ```bash
    javadoc -classpath ./libs -d ./doc Person.java
    ```
    
- `-subpackages` : Permet de documenter tous les fichiers Java d’un package et de ses sous-packages.  
    **Exemple :**
    
    ```bash
    javadoc -d ./doc -subpackages com.example
    ```
    
- `-author` : Ajoute la section "Author" dans la documentation générée si la balise `@author` est utilisée.  
    **Exemple :**
    
    ```bash
    javadoc -d ./doc -author Person.java
    ```
    
- `-version` : Inclut la section "Version" dans la documentation si la balise `@version` est utilisée.  
    **Exemple :**
    
    ```bash
    javadoc -d ./doc -version Person.java
    ```
    
- `-private` : Génère la documentation pour tous les éléments (y compris ceux marqués comme `private`). Par défaut, seuls les éléments `public` et `protected` sont documentés.  
    **Exemple :**
    
    ```bash
    javadoc -d ./doc -private Person.java
    ```
    

### Exemple complet
Pour documenter un projet contenant plusieurs fichiers Java, vous pouvez utiliser une commande combinée :

```bash
javadoc -d ./doc -sourcepath ./src -subpackages com.example -author -version
```

Cette commande génère une documentation complète pour tous les fichiers dans le package `com.example` et ses sous-packages, tout en incluant les informations sur l’auteur et la version.

### Visualiser la documentation générée
Une fois la commande exécutée, vous pouvez ouvrir le fichier `index.html` situé dans le dossier spécifié (par exemple, `./doc`) pour consulter la documentation dans un navigateur.

```bash
open ./doc/index.html  # Sur macOS/Linux
start ./doc/index.html # Sur Windows
```

### Astuce : Automatiser avec un script
Pour des projets plus complexes, vous pouvez automatiser la génération de documentation avec un script. Exemple pour un script Bash :

```bash
#!/bin/bash
javadoc -d ./doc -sourcepath ./src -subpackages com.example -author -version
echo "Documentation générée dans le dossier ./doc"
```