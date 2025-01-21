
---

### Thème du Projet

**[ Clustering avec la méthode K-means]**

---

### Préparé par :



- Salif Biaye

- Mouhamadou Tidiane Seck

- Ouleymatou Sadiya Cisse

- Ndeye Astou Diagouraga

---

### Encadrant :

**Professeur Mamadou Camara**

---

### Année Académique

**[2023-2024]**

---
# Sommaire

1. *Introduction*
    
    - Présentation des objectifs et du contexte du TP.
    - Description des jeux de données utilisés :
        - Mesures de pluviométrie dans les régions du Sénégal.
        - Base de données Iris.
2. *Partie 1 : K-means sur des données de pluviométrie*  
    2.1. *Différences entre les deux codes*
    
    - Explications détaillées des distinctions dans l'initialisation des centres des clusters.  
        2.2. *Impact sur la convergence*
    - Comparaison de la convergence et des résultats pour chaque approche.  
        2.3. *Conclusion sur les deux approches*
    - Avantages et inconvénients des deux codes.
3. *Partie 2 : K-means sur la base Iris*
    3.1. *Explication des différences entre les deux codes*
    
    - Comparaison des données et de l'initialisation.  
        3.2. *Analyse des itérations nécessaires pour la convergence*
    - Discussion sur la stabilité et les résultats obtenus.  
        3.3. *Vérification des résultats similaires*
    - Observations sur la convergence et les similarités des clusters formés.
4. *Comparaison globale des deux versions de code* 
    4.1. *Initialisation fixe vs adaptative*
    
    - Avantages et inconvénients de chaque approche.  
        4.2. *Analyse des résultats et visualisations*
    - Comparaison des performances sur les deux ensembles de données.


---

## Introduction
Ce TP porte sur l'utilisation de la méthode de clustering K-means pour analyser des données. Nous allons explorer deux jeux de données :
- Les mesures de pluviométrie dans les régions du Sénégal.
- La base Iris, un jeu de données classique en apprentissage machine.

## Partie 1 : K-means sur des données de pluviométrie

### Différences entre les deux codes

Les deux codes sont très similaires dans leur structure, mais une différence clé réside dans la manière dont les centres initiaux des clusters sont déterminés.

1. premier code
```R
base::setwd("./")  
library(cluster)  
lecture <- function(file) {  
    read.table(file, header=T, sep='', dec=',') ;  
}  
#lecture du fichier des données  
mydata <- lecture("exemple1.txt") ;  
  
#initialisation de la zone de dessin (découpage en 2 lignes et 3 colonnes )  
par(mfrow=c(2,3))  
  
fit1 <- kmeans(mydata, 5, iter.max=2) # solution à 5 cluster  
  
# Faire correspondre les individus avec leur cluster approprié dans la solution.  
# data.frame fait un append et écrase mydata  
mydata <- data.frame(mydata, fit1$cluster)  
  
# Schema du cluster Plot  
clusplot(mydata[, 1:16], fit1$cluster, color=TRUE, shade=TRUE, labels=2, lines=0)  
  
for(i in 3:7){ #Faire successivement les itérations pour bien observer la différence d  
    # Analyse de clustering par K-Mean   
     fit2 <- kmeans(mydata[, 1:16], 5, iter.max=i) # solution à 5 cluster  
  
    # Faire correspondre les individus avec leur cluster approprié dans la solution.   
     # data.frame fait un append et écrase mydata   
      mydata <- data.frame(mydata, fit2$cluster)  
  
    # Schema du cluster Plot  
    clusplot(mydata[, 1:16], fit2$cluster, color=TRUE, shade=TRUE, labels=2, lines=0)  
}  
  
dis <- dist(mydata[, 1:16])
```

2. deuxième code
```R
base::setwd("./")  
library(cluster)  
lecture <- function(file) {  
    read.table(file, header=T, sep='', dec=',') ;  
}  
#lecture du fichier des données  
mydata <- lecture("exemple1.txt") ;  
  
#initialisation de la zone de dessin (découpage en 2 lignes et 3 colonnes )  
par(mfrow=c(2,3))  
numlignecentres<-c(5,23,25,28,29)  
lignescentres<-mydata[numlignecentres,1:16]  
  
fit1 <- kmeans(mydata, lignescentres, iter.max=2) # solution à 5 cluster  
  
# Faire correspondre les individus avec leur cluster approprié dans la solution.  
# data.frame fait un append et écrase mydata  
mydata <- data.frame(mydata, fit1$cluster)  
  
# Schema du cluster Plot  
clusplot(mydata[, 1:16], fit1$cluster, color=TRUE, shade=TRUE, labels=2, lines=0)  
  
for(i in 3:7){ #Faire successivement les itérations pour bien observer la différence d  
    # Analyse de clustering par K-Mean    
    fit2 <- kmeans(mydata[, 1:16], lignescentres, iter.max=i) # solution à 5 cluster  
  
    # Faire correspondre les individus avec leur cluster approprié dans la solution.    
    # data.frame fait un append et écrase mydata    
    mydata <- data.frame(mydata, fit2$cluster)  
  
    # Schema du cluster Plot  
    clusplot(mydata[, 1:16], fit2$cluster, color=TRUE, shade=TRUE, labels=2, lines=0)  
}  
mydata
```

---

### Différence principale

1. **Premier code** :
    
    - Les centres initiaux des clusters sont choisis **aléatoirement** par l'algorithme `kmeans`.
    - À chaque itération, les centres sont réinitialisés de manière différente, ce qui peut conduire à des résultats variables entre les itérations.
2. **Second code** :
    
    - Les centres initiaux des clusters sont spécifiés explicitement via les lignes `numlignecentres` extraites du dataset (`mydata[numlignecentres, 1:16]`).
    - Cela fournit des points de départ fixes pour l'algorithme, garantissant que les calculs démarrent toujours au même endroit. Cela réduit les variations dues à l'initialisation aléatoire.

---

### Impact sur la convergence

- **Premier code** :  
    Comme les centres initiaux sont aléatoires, l'algorithme peut :
    
    1. Converger vers des solutions différentes à chaque exécution, dépendant fortement de l'initialisation.
    2. Nécessiter davantage d'itérations pour atteindre une solution stable, car les centres peuvent démarrer loin des clusters réels.
- **Second code** :  
    Avec des centres initiaux fixes (sélectionnés dans `numlignecentres`), l'algorithme démarre à partir d'un point de départ cohérent et proche des clusters attendus. Cela améliore :
    
    1. La **stabilité** : Les résultats sont moins sensibles à l'initialisation aléatoire.
    2. La **rapidité de convergence** : Les centres étant bien placés dès le départ, l'algorithme atteint une solution stable en moins d'itérations.

---

### Convergence notée dans le second code

1. **Origine** : La convergence observée dans le second code provient de l'utilisation de centres initiaux définis (`numlignecentres`). Ces centres sont bien choisis, ce qui réduit les déplacements des centroids au cours des itérations.
    
2. **En comparaison avec le premier code** :
    
    - Dans le premier code, l'aléatoire peut placer les centres initiaux loin des clusters réels, nécessitant plusieurs itérations pour ajuster les centroïdes.
    - Dans le second code, les centres sont définis proche des clusters, ce qui accélère l'ajustement et stabilise rapidement les clusters.

---

### Conclusion

- La principale différence est l'initialisation des centres des clusters.
- **Premier code** : Initialisation aléatoire → Résultats variables, convergence plus lente.
- **Second code** : Initialisation déterministe (fixe) → Résultats stables, convergence rapide.
---
## Partie 2 : K-means sur la base Iris
### Expliquer la différence entre le code ci-dessous et le précédant

-  **Nombre d'itérations nécessaires**
    
    - **Premier code** : La convergence est observée dès la **2e itération**, grâce à une meilleure sélection des centres initiaux.
    
 ```R
base::setwd("./")  
library(cluster)  
lecture <- function(file) {  
    read.table(file, header=T, sep='', dec=',') ;  
}  
#lecture du fichier des données  
mydata <- lecture("exemple1.txt") ;  
  
#initialisation de la zone de dessin (découpage en 2 lignes et 3 colonnes )  
par(mfrow=c(2,3))  
numlignecentres<-c(5,23,25,28,29)  
lignescentres<-mydata[numlignecentres,1:16]  
  
fit1 <- kmeans(mydata, lignescentres, iter.max=2) # solution à 5 cluster  
  
# Faire correspondre les individus avec leur cluster approprié dans la solution.  
# data.frame fait un append et écrase mydata  
mydata <- data.frame(mydata, fit1$cluster)  
  
# Schema du cluster Plot  
clusplot(mydata[, 1:16], fit1$cluster, color=TRUE, shade=TRUE, labels=2, lines=0)  
  
for(i in 3:7){ #Faire successivement les itérations pour bien observer la différence d  
    # Analyse de clustering par K-Mean    
    fit2 <- kmeans(mydata[, 1:16], lignescentres, iter.max=i) # solution à 5 cluster  
  
    # Faire correspondre les individus avec leur cluster approprié dans la solution.    
    # data.frame fait un append et écrase mydata    
    mydata <- data.frame(mydata, fit2$cluster)  
  
    # Schema du cluster Plot  
    clusplot(mydata[, 1:16], fit2$cluster, color=TRUE, shade=TRUE, labels=2, lines=0)  
}  
mydata
```

![[cluster1 1.png]]

- **Deuxième code** : La convergence est observée à partir de **3 itérations**. Cela pourrait être dû au choix  des centres initiaux qui nécessitent plus d'ajustements.

```R
library(cluster)  
samp <- c(27, 53, 69, 104, 136,87,150, 73, 114, 75, 126, 108, 54, 80, 143, 84, 94, 5,  
          92, 138,111, 63, 76, 83, 57, 23,18,7, 125, 32, 110, 107, 134, 105, 119, 147, 22, 25,  
          141,29, 131, 122, 60, 64, 81, 95,45, 149, 48, 3, 13, 14, 77, 135, 68, 145, 4)  
 s <- c(56,17,1,50,42,4,22,24)  
  
  
mydata <- iris[samp, 1:4]  
#mydata <- iris[1:50, 1:4]  
#mydata  
par(mfrow = c(3, 3))  
s  
c <- mydata[s, 1:4]  
  
fit1 <- kmeans(mydata, centers = c, iter.max = 1) # solution à 5 cluster  
  
# Faire correspondre les individus avec leur cluster approprié dans la solution.  
# data.frame fait un append et écrase mydata  
mydata <- data.frame(mydata, fit1$cluster)  
  
# Schema du cluster Plot  
clusplot(mydata[, 1:4], fit1$cluster, color = TRUE, shade = TRUE, labels = 2, lines = 0)  
  
for (i in 2:9) { # Faire successivement les itérations pour bien observer la différence des modèles  
  # Analyse de clustering par K-Mean  
  fit <- kmeans(mydata[, 1:4], centers = c, iter.max = i) # solution à 5 cluster  
  
  # Faire correspondre les individus avec leur cluster approprié dans la solution.  
  # data.frame fait un append et écrase mydata  
  mydata <- data.frame(mydata, fit$cluster)  
  
  # Schema du cluster Plot  
  clusplot(mydata[, 1:4], fit$cluster, color = TRUE, shade = TRUE, labels = 2, lines = 0)  
}  
```

![[cluster2 2.png]]

#### Différences principales

1. **Sélection des centres initiaux**
    
    - **Premier code**
        - Les centres initiaux sont **manuellement spécifiés** à partir de lignes spécifiques de l’ensemble de données (`numlignecentres <- c(5, 23, 25, 28, 29)`).
        - Cela permet de démarrer avec des centres possiblement bien distribués, favorisant une convergence rapide (2 itérations seulement).
    - **Deuxième code**
        - Les centres initiaux sont sélectionnés à l'aide d'un **échantillon aléatoire** d'indices (`s <- c(56, 17, 1, 50, 42, 4, 22, 24)`), ce qui introduit une certaine variabilité.
        - Cela peut nécessiter plus d'ajustements (3 ou plus d'itérations) pour obtenir des clusters stables.
2. **Données utilisées**
    
    - **Premier code**
        - Les données sont extraites d’un fichier externe, et seules les **16 premières colonnes** sont utilisées pour le clustering.
    - **Deuxième code**
        - Les données proviennent de l’ensemble prédéfini `iris`, limité à 4 dimensions correspondant aux colonnes 1 à 4.
3. **Nombre d’itérations et observation de la convergence**
    
    - **Premier code**
        - La convergence est atteinte rapidement, dès **2 itérations**, grâce à des centres bien choisis.
    - **Deuxième code**
        - La convergence nécessite **plus d'itérations** (à partir de 3), probablement en raison du choix initial aléatoire des centres, nécessitant davantage d'ajustements.
4. **Complexité des visualisations**
    
    - **Premier code**
        - Génère 6 graphiques correspondant aux différentes itérations (de 3 à 7).
    - **Deuxième code**
        - Produit 9 visualisations (de 2 à 9 itérations), offrant une vue plus détaillée de l’évolution.

### vérifier que les deux versions de code donnent le même résultat 

- première version : Chaque itération réinitialise les centres des clusters à ceux prédéfinis (à l’aide de la variable `c`).

```R
library(cluster)  
samp <- c(27, 53, 69, 104, 136,87,150, 73, 114, 75, 126, 108, 54, 80, 143, 84, 94, 5,  
          92, 138,111, 63, 76, 83, 57, 23,18,7, 125, 32, 110, 107, 134, 105, 119, 147, 22, 25,  
          141,29, 131, 122, 60, 64, 81, 95,45, 149, 48, 3, 13, 14, 77, 135, 68, 145, 4)  
 s <- c(56,17,1,50,42,4,22,24)  
  
  
mydata <- iris[samp, 1:4]  
#mydata <- iris[1:50, 1:4]  
#mydata  
par(mfrow = c(3, 3))  
s  
c <- mydata[s, 1:4]  
  
fit1 <- kmeans(mydata, centers = c, iter.max = 1) # solution à 5 cluster  
  
# Faire correspondre les individus avec leur cluster approprié dans la solution.  
# data.frame fait un append et écrase mydata  
mydata <- data.frame(mydata, fit1$cluster)  
  
# Schema du cluster Plot  
clusplot(mydata[, 1:4], fit1$cluster, color = TRUE, shade = TRUE, labels = 2, lines = 0)  
  
for (i in 2:9) { # Faire successivement les itérations pour bien observer la différence des modèles  
  # Analyse de clustering par K-Mean  
  fit <- kmeans(mydata[, 1:4], centers = c, iter.max = i) # solution à 5 cluster  
  
  # Faire correspondre les individus avec leur cluster approprié dans la solution.  
  # data.frame fait un append et écrase mydata  
  mydata <- data.frame(mydata, fit$cluster)  
  
  # Schema du cluster Plot  
  clusplot(mydata[, 1:4], fit$cluster, color = TRUE, shade = TRUE, labels = 2, lines = 0)  
}  
```

- deuxième version : Les centres des clusters sont ajustés à chaque itération, ce qui permet une mise à jour progressive des centroïdes.

```R
library(cluster)  
samp <- c(27, 53, 69, 104, 136,87,150, 73, 114, 75, 126, 108, 54, 80, 143, 84, 94, 5,  
          92, 138,111, 63, 76, 83, 57, 23,18,7, 125, 32, 110, 107, 134, 105, 119, 147, 22, 25,  
          141,29, 131, 122, 60, 64, 81, 95,45, 149, 48, 3, 13, 14, 77, 135, 68, 145, 4)  
 s <- c(56,17,1,50,42,4,22,24)  
  
  
mydata <- iris[samp, 1:4]  
#mydata <- iris[1:50, 1:4]  
#mydata  
par(mfrow = c(3, 3))  
s  
c <- mydata[s, 1:4]  
  
fit <- kmeans(mydata, centers = c, iter.max = 1) # solution à 5 cluster  
  
# Faire correspondre les individus avec leur cluster approprié dans la solution.  
# data.frame fait un append et écrase mydata  
mydata <- data.frame(mydata, fit$cluster)  
  
# Schema du cluster Plot  
clusplot(mydata[, 1:4], fit$cluster, color = TRUE, shade = TRUE, labels = 2, lines = 0)  
  
for (i in 2:9) { # Faire successivement les itérations pour bien observer la différence des modèles  
  # Analyse de clustering par K-Mean
  fit <- kmeans(mydata[, 1:4], centers = fit$centers, iter.max = 1) # solution à 5 cluster  
  
  # Faire correspondre les individus avec leur cluster approprié dans la solution.  
  # data.frame fait un append et écrase mydata 
   mydata <- data.frame(mydata, fit$cluster)  
  
  # Schema du cluster Plot  
  clusplot(mydata[, 1:4], fit$cluster, color = TRUE, shade = TRUE, labels = 2, lines = 0)  
}  
mydata
```

#### Détails des différences

##### Premier code : Initialisation fixe à chaque itération

1. **Avantages** :
    
    - Plus rapide pour atteindre une solution, car les centres restent constants au départ de chaque itération.
        
    - Idéal si les centres initiaux sont proches des clusters réels.
        
2. **Inconvénients** :
    
    - Peut manquer de flexibilité si les centres initiaux sont mal choisis.
        
    - Résultats moins adaptatifs.
        

##### Deuxième code : Ajustement des centres à chaque itération

1. **Avantages** :
    
    - Plus adaptatif, car les centres évoluent à chaque itération en fonction des clusters identifiés.
        
    - Convergence plus robuste dans des situations où les centres initiaux sont mal positionnés.
        
2. **Inconvénients** :
    
    - Peut nécessiter plus d’itérations.
        
    - Plus coûteux en calculs.
        

### Comparaison des résultats

Les deux versions convergent vers des clusters similaires à partir de la 3e itération, comme observé dans les graphes. Cependant, l’approche adaptative du second code est plus élégante et mieux adaptée aux scénarios réels.

![[cluster2.png]]


---

