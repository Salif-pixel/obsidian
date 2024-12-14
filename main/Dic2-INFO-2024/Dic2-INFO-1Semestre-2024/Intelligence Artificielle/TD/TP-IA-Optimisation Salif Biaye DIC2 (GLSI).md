


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
from sklearn.metrics import accuracy_score
from sklearn.model_selection import GridSearchCV,RandomizedSearchCV
import optuna
from sklearn.model_selection import cross_val_score

```

---

## Chargement des données via un fichier csv

```python
# Charger les données
data = pd.read_csv("./datatest/DatasetmalwareExtrait.csv")

# Afficher les premières lignes
print(data.columns)
# Vérifier la répartition des classes
print(data.legitimate.value_counts())


```



## Séparation  des caractéristiques (X) et la cible (y) "legitimate" et division en ensemble d'entraînement

```python
# Séparer les caractéristiques (X) et la cible (y)
X = data.drop(columns=['legitimate'])  
y = data['legitimate']
# Diviser les données en ensemble d'entraînement et de test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42, stratify=y)
# afficher les resultats pour voir si il sont coherents
print(len(X_train), len(X_test), len(y_train), len(y_test))

```



## Évaluation - Arbre de Décision avec GridSearch


```python
#  Optimisation de l'arbre de décision 
param_grid_tree = {
    'criterion': ['gini', 'entropy'],         
    'max_depth': [None, 5, 10, 15],            
    'min_samples_split': [2, 5, 10],           
    'min_samples_leaf': [1, 2, 4]              
}

# Initialiser le modèle
dt_model = DecisionTreeClassifier(random_state=42)

grid_search_tree = GridSearchCV(
    estimator=dt_model,
    param_grid=param_grid_tree,
    scoring='accuracy',
    cv=5,  
    verbose=1,
    n_jobs=-1  
)
# Entraîner le modèle
grid_search_tree.fit(X_train, y_train)

print("\n Arbre de décision ")
print("Meilleurs hyperparamètres :", grid_search_tree.best_params_)
best_tree = grid_search_tree.best_estimator_
print("Précision sur l'ensemble de test :", accuracy_score(y_test, best_tree.predict(X_test)))
best_dt_params = grid_search_tree.best_params_

# Créer un modèle avec ces hyperparamètres
optimized_dt = DecisionTreeClassifier(**best_dt_params, random_state=42)
optimized_dt.fit(X_train, y_train) 

# Faire des prédictions
y_pred_dt = optimized_rf.predict(X_test)
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



## Évaluation - Forêt Aléatoire avec GridSearch

```python
#  Optimisation de la forêt aléatoire 
param_grid_rf = {
    'n_estimators': [50,100],             
    'criterion': ['gini', 'entropy'],        
    'max_depth': [None, 10,20],          
    'min_samples_split': [2, 5],           
    'min_samples_leaf': [1, 2],             
    'max_features': ['sqrt', 'log2'] 
}
# Initialiser le modèle
rf_model = RandomForestClassifier(random_state=42)

grid_search_rf = GridSearchCV(
    estimator=rf_model,
    param_grid=param_grid_rf,
    scoring='accuracy',
    cv=5,  
    verbose=1,
    n_jobs=-1  
)

grid_search_rf.fit(X_train, y_train)

print("\n Forêt aléatoire ")
print("Meilleurs hyperparamètres :", grid_search_rf.best_params_)
best_rf = grid_search_rf.best_estimator_
print("Précision sur l'ensemble de test :", accuracy_score(y_test, best_rf.predict(X_test)))

best_rf_params = grid_search_rf.best_params_

# Créer un modèle avec ces hyperparamètres
optimized_rf = RandomForestClassifier(**best_rf_params, random_state=42)
optimized_rf.fit(X_train, y_train)  # Réentraîner le modèle avec les données d'entraînement

# Faire des prédictions
y_pred_rf = optimized_rf.predict(X_test)

# === Évaluation du modèle ===
# Matrice de confusion
cm_rf = confusion_matrix(y_test, y_pred_rf)

# Afficher la heatmap de la matrice de confusion
plt.figure(figsize=(8, 6))
sns.heatmap(cm_rf, annot=True, fmt='d', cmap='Reds', xticklabels=['Non-Malware', 'Malware'], yticklabels=['Non-Malware', 'Malware'])
plt.xlabel('Prédictions')
plt.ylabel('Vérités')
plt.title('Matrice de Confusion - Random Forest')
plt.show()

# Rapport de classification
print("\nRapport de classification :\n", classification_report(y_test, y_pred_rf))
```



## Évaluation - Arbre de Décision avec RandomSearch

```python
#  Optimisation de l'arbre de décision 
param_grid_tree = {
    'criterion': ['gini', 'entropy'],         
    'max_depth': [None, 5, 10, 15],            
    'min_samples_split': [2, 5, 10],           
    'min_samples_leaf': [1, 2, 4]              
}

# Initialiser le modèle
dt_model = DecisionTreeClassifier(random_state=42)

random_search_dt = RandomizedSearchCV(
    estimator=dt_model,
    param_distributions=param_grid_tree,
    n_iter=20,  
    scoring='accuracy',
    cv=5, 
    verbose=1,
    random_state=42,
    n_jobs=-1  
)

# Entraîner le modèle
random_search_dt.fit(X_train, y_train)

print("\n Arbre de décision ")
print("Meilleurs hyperparamètres :", random_search_dt.best_params_)
best_tree = random_search_dt.best_estimator_
print("Précision sur l'ensemble de test :", accuracy_score(y_test, best_tree.predict(X_test)))
best_dt_params = random_search_dt.best_params_

# Créer un modèle avec ces hyperparamètres
optimized_dt = DecisionTreeClassifier(**best_dt_params, random_state=42)
optimized_dt.fit(X_train, y_train)  # Réentraîner le modèle avec les données d'entraînement

# Faire des prédictions
y_pred_dt = optimized_dt.predict(X_test)
# Évaluer le modèle

cm = confusion_matrix(y_test, y_pred_dt)
# Afficher la heatmap
plt.figure(figsize=(8, 6))
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', xticklabels=['Non-Malware', 'Malware'], yticklabels=['Non-Malware', 'Malware'])
plt.xlabel('Prédictions')
plt.ylabel('Vérités')
plt.title('Matrice de Confusion - Arbre de Décision')
plt.show()
print(classification_report(y_test, y_pred_dt))
```



## Évaluation - Forêt Aléatoire avec RandomSearch

```python
#  Optimisation de la forêt aléatoire 
param_grid_rf = {
    'n_estimators': [50,100],             
    'criterion': ['gini', 'entropy'],        
    'max_depth': [None, 10,20],          
    'min_samples_split': [2, 5],           
    'min_samples_leaf': [1, 2],             
    'max_features': ['sqrt', 'log2']  
}
# Initialiser le modèle
rf_model = RandomForestClassifier(random_state=42)

random_search_rf = RandomizedSearchCV(
    estimator=rf_model,
    param_distributions=param_grid_rf,
    n_iter=20,  
    scoring='accuracy',
    cv=5,  
    verbose=1,
    random_state=42,
    n_jobs=-1  
)

random_search_rf.fit(X_train, y_train)

print("\n Forêt aléatoire ")
print("Meilleurs hyperparamètres :", random_search_rf.best_params_)
best_rf = random_search_rf.best_estimator_
print("Précision sur l'ensemble de test :", accuracy_score(y_test, best_rf.predict(X_test)))

best_rf_params = random_search_rf.best_params_

# Créer un modèle avec ces hyperparamètres
optimized_rf = RandomForestClassifier(**best_rf_params, random_state=42)
optimized_rf.fit(X_train, y_train)  

# Faire des prédictions
y_pred_rf = optimized_rf.predict(X_test)

# === Évaluation du modèle ===
# Matrice de confusion
cm_rf = confusion_matrix(y_test, y_pred_rf)

# Afficher la heatmap de la matrice de confusion
plt.figure(figsize=(8, 6))
sns.heatmap(cm_rf, annot=True, fmt='d', cmap='Greens', xticklabels=['Non-Malware', 'Malware'], yticklabels=['Non-Malware', 'Malware'])
plt.xlabel('Prédictions')
plt.ylabel('Vérités')
plt.title('Matrice de Confusion - Random Forest')
plt.show()

# Rapport de classification
print("\nRapport de classification :\n", classification_report(y_test, y_pred_rf))
```



## Évaluation - Arbre de Décision avec Optuna


```python
# Fonction d'optimisation
def objective(trial):
    # Définir les hyperparamètres à optimiser
    criterion = trial.suggest_categorical('criterion', ['gini', 'entropy'])
    max_depth = trial.suggest_int('max_depth', 5, 15, step=5)
    min_samples_split = trial.suggest_int('min_samples_split', 2, 10, step=1)
    min_samples_leaf = trial.suggest_int('min_samples_leaf', 1, 4, step=1)

    # Initialiser le modèle avec ces hyperparamètres
    model = DecisionTreeClassifier(
        criterion=criterion,
        max_depth=max_depth,
        min_samples_split=min_samples_split,
        min_samples_leaf=min_samples_leaf,
        random_state=42
    )

    # Utiliser la validation croisée pour évaluer le modèle
    score = cross_val_score(model, X_train, y_train, n_jobs=-1, cv=5, scoring='accuracy')
    
    # Retourner la moyenne des scores de validation croisée comme objectif
    return score.mean()

# Créer une étude Optuna
study = optuna.create_study(direction='maximize')

# Lancer l'optimisation
study.optimize(objective, n_trials=40)

# Afficher les meilleurs hyperparamètres
print("Meilleurs hyperparamètres trouvés :", study.best_params)

# Créer un modèle avec les meilleurs hyperparamètres
best_params = study.best_params
optimized_dt = DecisionTreeClassifier(**best_dt_params,random_state=42)

# Entraîner le modèle
optimized_dt.fit(X_train, y_train)

# Faire des prédictions
y_pred_dt = optimized_dt.predict(X_test)

# Évaluer le modèle
print("Précision sur l'ensemble de test :", accuracy_score(y_test, y_pred_dt))

cm = confusion_matrix(y_test, y_pred_dt)

# Afficher la heatmap
plt.figure(figsize=(8, 6))
sns.heatmap(cm, annot=True, fmt='d', cmap='Purples', xticklabels=['Non-Malware', 'Malware'], yticklabels=['Non-Malware', 'Malware'])
plt.xlabel('Prédictions')
plt.ylabel('Vérités')
plt.title('Matrice de Confusion - Arbre de Décision')
plt.show()

# Afficher le rapport de classification
print(classification_report(y_test, y_pred_dt))
```



## Évaluation - Random Forest avec Optuna

```python
# Fonction d'optimisation
def objective(trial):
    # Définir les hyperparamètres à optimiser
    n_estimators = trial.suggest_int('n_estimators', 50, 100)
    criterion = trial.suggest_categorical('criterion', ['gini', 'entropy'])
    max_depth = trial.suggest_int('max_depth', 5, 15, step=5)
    min_samples_split = trial.suggest_int('min_samples_split', 2, 10, step=1)
    min_samples_leaf = trial.suggest_int('min_samples_leaf', 1, 4, step=1)
    max_features = trial.suggest_categorical('max_features', ['sqrt', 'log2'])

    # Initialiser le modèle avec ces hyperparamètres
    model = RandomForestClassifier(
        n_estimators=n_estimators,
        criterion=criterion,
        max_depth=max_depth,
        min_samples_split=min_samples_split,
        min_samples_leaf=min_samples_leaf,
        max_features=max_features,
        random_state=42
    )

    # Utiliser la validation croisée pour évaluer le modèle
    score = cross_val_score(model, X_train, y_train, n_jobs=-1, cv=5, scoring='accuracy')
    
    # Retourner la moyenne des scores de validation croisée comme objectif
    return score.mean()

# Créer une étude Optuna
study = optuna.create_study(direction='maximize')

# Lancer l'optimisation
study.optimize(objective, n_trials=20)

# Afficher les meilleurs hyperparamètres
print("Meilleurs hyperparamètres trouvés :", study.best_params)

# Créer un modèle avec les meilleurs hyperparamètres
best_params = study.best_params
optimized_rf = RandomForestClassifier(**best_dt_params,random_state=42)

# Entraîner le modèle
optimized_rf.fit(X_train, y_train)

# Faire des prédictions
y_pred_rf = optimized_rf.predict(X_test)

# Évaluer le modèle
print("Précision sur l'ensemble de test :", accuracy_score(y_test, y_pred_dt))

cm = confusion_matrix(y_test, y_pred_rf)

# Afficher la heatmap
plt.figure(figsize=(8, 6))
sns.heatmap(cm, annot=True, fmt='d', cmap='Pinks', xticklabels=['Non-Malware', 'Malware'], yticklabels=['Non-Malware', 'Malware'])
plt.xlabel('Prédictions')
plt.ylabel('Vérités')
plt.title('Matrice de Confusion - Random Forest')
plt.show()

# Afficher le rapport de classification
print(classification_report(y_test, y_pred_rf))

```

---

### **GridSearchCV**
- **Principe** : Essaie **toutes les combinaisons possibles** des hyperparamètres spécifiés dans un dictionnaire (`param_grid`).
- **Avantages** :
  - Exhaustif : il garantit que toutes les combinaisons sont testées.
  - Convient pour des espaces de recherche relativement petits.
- **Inconvénients** :
  - Très coûteux en temps de calcul si l'espace des hyperparamètres est grand (croissance exponentielle).
  - Peut tester des combinaisons inutiles si certaines zones de l'espace ne sont pas prometteuses.

### **RandomizedSearchCV**
- **Principe** : Sélectionne un **sous-ensemble aléatoire** de combinaisons d'hyperparamètres, basé sur un nombre spécifié d'itérations (`n_iter`).
- **Avantages** :
  - Plus rapide pour des espaces de recherche larges ou complexes.
  - Peut trouver des résultats similaires à GridSearchCV avec moins de calculs, car il explore rapidement plusieurs zones de l'espace.
- **Inconvénients** :
  - Pas exhaustif : certaines bonnes combinaisons pourraient ne pas être testées.
  - La qualité du résultat dépend du nombre d'itérations et de l'échantillonnage aléatoire.

### **Optuna**

**Principe :**
Optuna est un framework d'optimisation d'hyperparamètres qui utilise des méthodes d'optimisation bayésienne pour explorer de manière plus intelligente l'espace des hyperparamètres. Il choisit les combinaisons les plus prometteuses d'hyperparamètres en fonction des résultats précédents et améliore sa stratégie au fil des essais.

**Avantages :**
- **Efficacité** : Utilise une optimisation bayésienne (par exemple, TPE ou CMA-ES) pour explorer l'espace des hyperparamètres plus efficacement que GridSearchCV et RandomizedSearchCV.
- **Pruning** : Possède un mécanisme de pruning intégré, permettant d'arrêter les essais non prometteurs avant la fin, ce qui permet de gagner du temps et des ressources.
- **Exploration intelligente** : Concentres les essais sur les zones les plus prometteuses de l'espace des hyperparamètres en apprenant des essais précédents.
- **Flexibilité** : Permet d'optimiser non seulement des hyperparamètres discrets, mais aussi des distributions continues et conditionnelles.
- **Résultats rapides** : Peut trouver des hyperparamètres de bonne qualité en moins de temps que les méthodes exhaustives comme GridSearchCV, en particulier pour des espaces larges.

**Inconvénients :**
- **Complexité** : Plus complexe à configurer et à comprendre, surtout pour des utilisateurs débutants ou dans des situations simples.
- **Dépendance au nombre de `trials`** : Comme RandomizedSearchCV, la qualité de l'optimisation dépend du nombre d'essais (trials) effectués, bien que la méthode d'optimisation guide les essais pour être plus efficaces.
- **Temps de setup** : La mise en place d'Optuna peut demander plus de temps, car elle nécessite une fonction objectif et la gestion de l'étude.


