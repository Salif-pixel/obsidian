

## Introduction
Ce rapport documente les analyses et scripts réalisés dans le cadre du projet IA. Le contenu est structuré en sections distinctes avec des illustrations et des visualisations.

### TP-IA Salif Biaye DIC2 (GLSI)


---


## Import des différentes bibliothèques

```python
import pandas as pd
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
import matplotlib.pyplot as plt
from sklearn.metrics import confusion_matrix, classification_report

```

 ---

### Chargement des données via un fichier csv

```python
# Charger les données
data = pd.read_csv("./datatest/DatasetmalwareExtrait.csv")

# Afficher les premières lignes
print(data.columns)
# Vérifier la répartition des classes
print(data.legitimate.value_counts())


```

#### Résultats
```
Index(['AddressOfEntryPoint', 'MajorLinkerVersion', 'MajorImageVersion',
       'MajorOperatingSystemVersion', 'DllCharacteristics',
       'SizeOfStackReserve', 'NumberOfSections', 'ResourceSize', 'legitimate'],
      dtype='object')
legitimate
0    96526
1    40918
Name: count, dtype: int64
```

---

###  Séparation  des caractéristiques (X) et la cible (y) "legitimate"

```python
# Séparer les caractéristiques (X) et la cible (y)
X = data.drop(columns=['legitimate'])  
y = data['legitimate']
# Diviser les données en ensemble d'entraînement et de test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42, stratify=y)
# afficher les resultats pour voir si il sont coherents
print(len(X_train), len(X_test), len(y_train), len(y_test))

```

#### Résultats
```
109955 27489 109955 27489
```

 ---

###  Évaluation - Arbre de Décision

```python
# Initialiser le modèle
dt_model = DecisionTreeClassifier(random_state=42)

# Entraîner le modèle
dt_model.fit(X_train, y_train)

# Faire des prédictions
y_pred_dt = dt_model.predict(X_test)

# Évaluer le modèle

cm = confusion_matrix(y_test, y_pred_dt)
# Afficher la heatmap
plt.figure(figsize=(8, 6))
sns.heatmap(cm, annot=True, fmt='d', cmap='Oranges', xticklabels=['Non-Malware', 'Malware'], yticklabels=['Non-Malware', 'Malware'])
plt.xlabel('Prédictions')
plt.ylabel('Vérités')
plt.title('Matrice de Confusion - Arbre de Décision')
plt.show()
print(classification_report(y_test, y_pred_dt))

```

#### Résultats
```
              precision    recall  f1-score   support

           0       0.99      0.99      0.99     19305
           1       0.98      0.98      0.98      8184

    accuracy                           0.99     27489
   macro avg       0.98      0.99      0.99     27489
weighted avg       0.99      0.99      0.99     27489

```

---

###  Évaluation - Forêt Aléatoire

```python
# Initialiser le modèle
rf_model = RandomForestClassifier(n_estimators=100, random_state=42)

# Entraîner le modèle
rf_model.fit(X_train, y_train)

# Faire des prédictions
y_pred_rf = rf_model.predict(X_test)

# Évaluer le modèle

cm_rf = confusion_matrix(y_test, y_pred_rf)
# Afficher la heatmap
plt.figure(figsize=(8, 6))
sns.heatmap(cm_rf, annot=True, fmt='d', cmap='Greens', xticklabels=['Non-Malware', 'Malware'], yticklabels=['Non-Malware', 'Malware'])
plt.xlabel('Prédictions')
plt.ylabel('Vérités')
plt.title('Matrice de Confusion - Random Forest')
plt.show()
print(classification_report(y_test, y_pred_rf))

```

#### Résultats
```
              precision    recall  f1-score   support

           0       0.99      0.99      0.99     19305
           1       0.99      0.99      0.99      8184

    accuracy                           0.99     27489
   macro avg       0.99      0.99      0.99     27489
weighted avg       0.99      0.99      0.99     27489

```

 ---


###  Conclusion entre ces deux méthodes
À partir des résultats obtenus, voici une analyse comparative et une suggestion de conclusion :

---

### **1. Résultats des modèles :**

#### **Decision Tree (Arbre de décision)** :
- **Classe 0 (Non Malware)** :
  - **Precision** : 0.99
  - **Recall** : 0.99
  - **F1-score** : 0.99
  - **Support** : 19 305 échantillons.

- **Classe 1 (Malware)** :
  - **Precision** : 0.98
  - **Recall** : 0.98
  - **F1-score** : 0.98
  - **Support** : 8 184 échantillons.


---

#### **Random Forest (Forêt aléatoire)** :
- **Classe 0 (Non Malware)** :
  - **Precision** : 0.99
  - **Recall** : 0.99
  - **F1-score** : 0.99
  - **Support** : 19 305 échantillons.

- **Classe 1 (Malware)** :
  - **Precision** : 0.99
  - **Recall** : 0.99
  - **F1-score** : 0.99
  - **Support** : 8 184 échantillons.



---

### **2. Comparaison directe :**

| **Métrique**   | **Decision Tree** | **Random Forest** |
|----------------|-------------------|-------------------|
| **Accuracy**   | 0.99              | 0.99              |
| **Precision (classe 1)** | 0.98              | 0.99              |
| **Recall (classe 1)**    | 0.98              | 0.99              |
| **F1-score (classe 1)**  | 0.98              | 0.99              |
| **Macro Average**        | 0.98              | 0.99              |

---



### **Conclusion rédigée :**
> Après avoir comparé les performances des deux modèles, **Random Forest** et **Decision Tree**, nous constatons que les deux obtiennent une précision globale de **99%**. Cependant, le **Random Forest** montre des résultats légèrement supérieurs en termes de précision, recall et F1-score pour détecter les malwares (classe 1).  





