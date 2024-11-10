

---

# Java

## Encapsulation
L'encapsulation permet de séparer chaque objet en deux parties : l'interface et l'implémentation (structure). Elle gère l'intégrité des objets :
- **Interface** : Partie visible qui permet à un objet d'interagir avec d'autres objets. Les objets communiquent entre eux via l'interface.
- **Implémentation** : Partie cachée que les autres objets n'ont pas besoin de connaître. Elle contient tout ce qui est essentiel mais inaccessible de l'extérieur.

## Classification et Héritage
- **Classification** : Organise les classes et peut donner naissance à de nouvelles classes.
- **Généralisation** : Mouvement par lequel des superclasses sont créées à partir de sous-classes (dans la conception).
- **Spécialisation** : Processus inverse de la généralisation.
  
La généralisation et la spécialisation se basent sur **l'héritage**, le mécanisme par lequel une sous-classe hérite d'une partie d'une superclasse.

## Tips
### Outils de Gestion de Distribution (Outils de Gestion de Configurations)
Exemples :
- **Make en C** : Identifier les modules et créer un `makefile` pour exécuter les commandes de compilation.
- **Gradle en Java**
- **Ant d'Apache**

### Exemple
Construire une classe pour gérer les fractions.

## Concepts Avancés
- **Polymorphisme** : Lorsqu'un objet change de comportement au cours de son cycle de vie.
- **Méthode de Classe** : Une méthode appelée sur la classe elle-même.
- **Abstraction** : Création de classes qui définissent des concepts sans entrer dans les détails de l'implémentation.
- **Instanciation** : Création d'objets, souvent avec l'opérateur `new`.
  
### Description
- **Par Intension** : Donner les caractéristiques, comme une relation en base de données.
- **Par Extension** : Énumérer les éléments.

## Variables et Constructeurs
- Toute **variable de type classe** est une **référence**.
- Un **constructeur** porte toujours le même nom que la classe, n'a pas de valeur de retour, et est toujours appelé avec l'opérateur `new`.
- Un **champ final** est constant ; une fois initialisé, il ne peut plus être modifié. S'il doit être différé, il doit être initialisé au plus tard lors de la construction de l'objet.

## Contrat et Comportement
- **Contrat** : Ensemble de services définis par les en-têtes de méthodes publiques et le comportement de ces méthodes. 
    - Le contrat définit ce que fait la classe.
    - **Implémentation** : Précise comment la classe réalise ce contrat.

## Copies
- **Copie Superficielle** : Copie seulement les références des objets.
- **Copie Profonde** : Crée une copie complète, y compris les objets internes.

### Exemple de Copie
- Classe `Programme`, `Cercle`, **Copie Superficielle** : `Point Cercle(c1.getRayon, c1.getCentre)`
- **Copie Profonde** : `Cercle(c1.getRayon, new Point(c1.getCentre))`