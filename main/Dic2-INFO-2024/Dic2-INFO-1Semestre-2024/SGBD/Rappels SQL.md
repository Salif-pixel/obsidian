
---


`**Structured Query Language**` est divisé en 3 langages :

- **LDD** : Langage de Définition de Données  
  Gérer les structures des informations qui sont stockées

- **LMD** : Langage de Manipulation de Données  
  Gérer les données qui sont stockées sans avoir à modifier leurs structures

- **LED** : Langage d’Extraction de Données  
  Permet d'extraire et mettre en forme les données qui sont renvoyées à l'utilisateur

En termes de syntaxe, les différents langages ont la même base :

**MOTCLEF:** `<Paramètres>`

**MOTCLEF:** `Primitive assertionelle qui donne un ordre au SGBD`
;  : Caractère de fin de commande par défaut (modifiable)

- LDD:
		CREATE
		ALTER
		DROP
- LMD:
		INSERT
		UPDATE
		DELETE
- LED:
		SELECT

On peut avoir les détails sur sa syntaxe dans MySQL . En utilisant Help suivit de la commande

SELECT `<Output>`
FROM `<INPUT>`
`[OPTIONS]`;

### `<Output>` :

- `*` : Tous les champs
- `<NomChamp>` : Champ choisi de façon explicite
- `DISTINCT <NomChamp>` : Permet d’éviter les répétitions
- `<Liste de Champs>` : Doivent être séparés par des virgules et l'ordre est personnalisé
- `<Constantes>` : Quelque soit le type de données de la constante
- `Reqimbriquees`: Requête  qui ne renverra qu'une seule valeur scalaire équivalente a une constante

### `[OPTIONS]`

- **LIMIT** : Permet de limiter le nombre d’enregistrements à afficher
    
    - `limit nbEnregistrements`
    - `limit Saut, nbEnregistrements`
- **ORDER BY** : Permet de trier les informations en fonction de champs choisis
    
    - `<champ> ASC / DESC` (ASC : Ascendant ; DESC : Descendant)
    - `<champ1>, <champ2>, <champ3>` (Par défaut, si aucun sens n’est cité, les champs sont triés en ASC)

### Exemple :

- Citer les 3 numéros d’employés les plus payés sans utiliser la fonction max
- `select emp_no, salary  from salaries order by salary DESC  limit 3;`
- Citer les 3 numéros d’employés les moins payés sans utiliser la fonction min
- `select DISTINCT emp_no, salary  from salaries order by salary ASC  limit 3;`

**Remarque** : Utiliser la table `salaries`

Mesurer la différence entre le salaire max et le salaire des employés en ne montrant que les 10 personnes qui sont les plus éloignés du salaire max.
`select  emp_no,((select max(salary) from salaries) - salary) as deltaSalary  from salaries`
	    `-> order by deltaSalary DESC limit 10;

- **GROUP BY** : permet de regrouper des enregistrements en fonction de valeurs de champ pour effectuer des calculs
### Exemple :
L'age moyen des employe
`select  avg(TIMESTAMPDIFF(YEAR,birth_date,CURDATE()))  from employees;`
`select  avg(Year(now()-year(birth_date)))  from employees;`
les 3 femmes les plus agees de l'entreprise
` select emp_no, TIMESTAMPDIFF(YEAR,birth_date,CURDATE())  as age from employees where gender= 'F' order by  age DESC limit 3 ;`
les 7 8 9 hommes les moins ages
`select emp_no, TIMESTAMPDIFF(YEAR,birth_date,CURDATE())  as age from employees where gender= 'M' order by  age ASC limit 6,3 ;`
les 5 employes les plus aciens et leur moyenne d'age
 `select emp_no , TIMESTAMPDIFF(YEAR,birth_date,CURDATE()) as age,    (SELECT AVG(TIMESTAMPDIFF(YEAR, birth_date, CURDATE()))`
    `->         FROM employees`
    `->         ORDER BY TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) DESC`
    `->         LIMIT 5) AS average_age`
    `->  from employees order by age DESC limit 5` ;`
A partir de titles quel est le numero d'employe qui a le plus dure dans un poste
 `select emp_no ,to_date-from_date as date from titles  order by date DESC limit 5;`