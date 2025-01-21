
---
## Sommaire

1. [Introduction](#introduction)

2. [Méthodes Utilisées](#méthodes-utilisées)

- [K-Means Clustering](#1-k-means-clustering)

- [BIRCH Clustering](#2-birch-clustering)

- [Gaussian Mixture Model (GMM)](#3-gaussian-mixture-model-gmm)

3. [Comparaison des Silhouette Scores](#comparaison-des-silhouette-scores)

4. [Conclusion](#conclusion)

---

## Introduction

Dans cette analyse, nous avons utilisé trois méthodes de clustering pour segmenter un jeu de données préalablement mis à l'échelle : K-Means, BIRCH et le modèle de Mélange Gaussien (GMM). L'objectif de cette analyse est de comparer la qualité des clusters formés par chacune de ces méthodes en utilisant le **Silhouette Score**, qui mesure la compacité et la séparation des clusters.

---

## Méthodes Utilisées

### 1. **K-Means Clustering**

Le K-Means est une méthode de clustering basée sur la partition des données en un nombre fixe de clusters, où chaque point appartient au cluster dont le centroïde est le plus proche. Nous avons utilisé `n_clusters=2` pour ce modèle.

```python
# 1. K-Means  
print("--- K-Means Clustering ---")  
kmeans = KMeans(n_clusters=2, random_state=42)  
kmeans_labels = kmeans.fit_predict(data_scaled)
```
#### Résultats du Silhouette Score pour K-Means

```python
Silhouette Score pour K-Means : 0.9931
```

### 2. **BIRCH Clustering**

BIRCH (Balanced Iterative Reducing and Clustering using Hierarchies) est une méthode de clustering hiérarchique qui est particulièrement efficace pour de grands ensembles de données. Elle utilise un arbre de clustering pour effectuer la segmentation. Nous avons également utilisé `n_clusters=2` pour cette méthode.

```python
# 2. BIRCH  
print("--- BIRCH Clustering ---")  
from sklearn.cluster import Birch  
birch = Birch(n_clusters=2)  
birch_labels = birch.fit_predict(data_scaled)
```

#### Résultats du Silhouette Score pour BIRCH

```python
Silhouette Score pour BIRCH : 0.9942
```

### 3. **Gaussian Mixture Model (GMM)**

Le modèle de Mélange Gaussien (GMM) est une approche probabiliste qui suppose que les données sont générées par un mélange de plusieurs distributions normales. Comme pour les autres méthodes, nous avons fixé `n_components=2` pour ce modèle.

#### Résultats du Silhouette Score pour GMM
```python
# 3. Gaussian Mixture Model (GMM)  
print("--- Gaussian Mixture Model (GMM) ---")  
gmm = GaussianMixture(n_components=2, random_state=42)  
gmm_labels = gmm.fit_predict(data_scaled)
```

```python
Silhouette Score pour GMM : 0.9931
```

---

## Comparaison des Silhouette Scores

Après avoir calculé le Silhouette Score pour chaque méthode, voici les résultats comparatifs :

```python
# Fonction pour calculer et afficher le Silhouette Score  
def calculate_silhouette_score(data_scaled, labels, method_name):  
    score = silhouette_score(data_scaled, labels)  
    print(f"Silhouette Score pour {method_name} : {score:.4f}")  
    return score
    
# Calcul du Silhouette Score pour K-Means  
kmeans_silhouette = calculate_silhouette_score(data_scaled, kmeans_labels, "K-Means")
# Calcul du Silhouette Score pour BIRCH  
birch_silhouette = calculate_silhouette_score(data_scaled, birch_labels, "BIRCH")
# Calcul du Silhouette Score pour GMM  
gmm_silhouette = calculate_silhouette_score(data_scaled, gmm_labels, "GMM")

# Comparaison des Silhouette Scores  
print("\nComparaison des Silhouette Scores :")  
print(f"K-Means Silhouette Score: {kmeans_silhouette:.4f}")  
print(f"BIRCH Silhouette Score: {birch_silhouette:.4f}")  
print(f"GMM Silhouette Score: {gmm_silhouette:.4f}")
```

| Méthode     | Silhouette Score |
| ----------- | ---------------- |
| **K-Means** | `0.9931`         |
| **BIRCH**   | `0.9942`         |
| **GMM**     | `0.9931`         |

Le Silhouette Score varie entre -1 et 1, où :

- **1** indique que les clusters sont bien séparés et distincts.
- **0** indique que les clusters sont trop proches et se chevauchent.
- **-1** indique que les points sont mal assignés aux clusters.

---

## Conclusion

En analysant les scores de chaque méthode, il est possible de déterminer laquelle est la plus efficace pour notre jeu de données. Un Silhouette Score plus élevé indique généralement une meilleure séparation des clusters. Il est recommandé de choisir la méthode qui donne le score le plus élevé pour garantir des clusters plus cohérents et mieux séparés donc ici la la méthode a choisir est le BIRCH.

---

