
----
si le `dataset` contient des variables non numérique, il faut les convertir en variable numérique. et pour cela on vérifie le type de la variable . autrement dit si c'est une variable nominale ou ordinale.

1. Variable ordinale : Exemple de variable d'appréciation (passable ,bien ,assez bien ,Excellent )
2. Variable nominale : on peut utiliser One hot encoder

	Stratégie de recherche d'optimisation des hyper paramètres :

- `gridsearch`
- `randomsearch`
- `optuna`