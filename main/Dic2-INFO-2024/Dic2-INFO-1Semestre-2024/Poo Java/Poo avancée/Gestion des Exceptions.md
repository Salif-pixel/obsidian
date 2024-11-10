

---

# Gestion des Exceptions

## Programmation Concurrentielle
Java prend en charge la programmation concurrentielle, permettant l'exécution de plusieurs tâches simultanément.

## Java 5 et la Programmation Générique
Java 5, introduit au milieu des années 2000, a introduit la **programmation générique**. Cela permet aux développeurs de créer des classes, interfaces et méthodes génériques, améliorant ainsi la sécurité de type et la réutilisabilité du code.

> [!NOTE]
> ## Gestion des Exceptions

- **Classe` Throwable` : Classe de base pour toutes les exceptions en Java. Elle se divise en deux sous-classes :
    - **Error** : Erreurs généralement irrécupérables.
    - **Exception** : Exceptions récupérables déclenchées par la JVM (Machine Virtuelle Java).

### Bloc `finally`
Le bloc `finally` est exécuté après le bloc `try-catch`, indépendamment de l'occurrence d'une exception. Cependant, il a peu d’intérêt lorsque les exceptions sont traitées localement.

## Gestion de la Mémoire
- **System.gc()** : Permet d’invoquer le **ramasse-miettes** (garbage collector) pour libérer de la mémoire non utilisée. 

---
[[Classes internes]]