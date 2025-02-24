
---


<div align="center">

### UNIVERSITÉ CHEIKH ANTA DIOP DE DAKAR  
*École Supérieure Polytechnique*  

</div>


<div style="text-align: center; padding: 20px;">

<div align="center">

![[logo_esp.png| 300]]

</div>

<div class="header" style="border: 3px double #1a5f7a; padding: 20px; margin: 20px 0;">

# ÉCOLE SUPÉRIEURE POLYTECHNIQUE DE DAKAR
## Département de Génie informatique

</div>


<div class="main-title" style="background-color: #f5f7fa; padding: 20px; border-radius: 10px; margin: 20px 0;">

# PROJET D'INTÉGRATION NUMÉRIQUE
## *Outils et méthodes mathématiques - Analyse numérique*

</div>

---

<div class="content" style="border-left: 3px solid #1a5f7a; border-right: 3px solid #1a5f7a; padding: 20px; margin: 20px 0;">

### Réalisé par :
- **Ouleymatou Sadiya CISSÉ  spécialité (SSI)**
- **Salif BIAYE spécialité (GLSI)**
- **Ndeye Astou DIAGOURAGA spécialité (SRT)**
- **Mouhamadou Tidiane SECK spécialité (GLSI)**

</div>

<div class="supervisor" style="background-color: #f5f7fa; padding: 15px; border-radius: 5px; margin: 20px 0;">

### Sous la direction de :
#### Dr SARR
*Enseignant*

</div>

---

<div  style="border: 3px double #1a5f7a; padding: 20px; margin: 20px 0;">

### Année universitaire 2024-2025
**

</div>

</div>
<div class="toc-container" style="background: linear-gradient(to right, #f8f9fa, #ffffff); border: 1px solid #e0e0e0; border-left: 4px solid #1a5f7a; border-radius: 8px; padding: 25px; margin: 20px 0; box-shadow: 0 2px 15px rgba(0,0,0,0.05);">

# Table des matières

### [[#Exercice 1 Interpolation de Lagrange pour un gaz en thermodynamique|📊 Exercice 1. Interpolation de Lagrange]]
- [[#I Données de l'expérience]]
- [[#II Méthode : Interpolation de Lagrange]]
- [[#III Calcul des polynômes de base de Lagrange]]
- [[#IV Calcul du polynôme final]]
- [[#V Approximation du volume spécifique pour P = 400 kPa]]

### [[#Exercice 2 Approximation de la Vitesse et de l'Accélération|📈 Exercice 2. Vitesse et Accélération]]
- [[#VI Méthodes numériques]]
  - [[#1 Approximation de la vitesse|1→ Approximation de la vitesse]]
  - [[#2 Approximation de l'accélération|2→ Approximation de l'accélération]]
- [[#VII Calculs]]
  - [[#1 Calcul des valeurs de x(t)|1→ Calcul des valeurs de x(t)]]
  - [[#2 Calcul de la vitesse approximée|2→ Calcul de la vitesse approximée]]
  - [[#3 Calcul de l'accélération approximée|3→ Calcul de l'accélération approximée]]
- [[#VIII Calcul des valeurs exactes]]
- [[#IX Comparaison des résultats]]

### [[#Exercice 3 Méthodes d'Intégration Numérique|∫ Exercice 3. Intégration Numérique]]
- [[#X Méthode des Points Milieux]]
- [[#XI Méthode des Trapèzes]]
- [[#XII Méthode de Simpson Composée]]

### [[#Exercice 4 Détermination de n pour la Méthode de Simpson|🎯 Exercice 4. Détermination de n]]
- [[#XIII Formule de l'Erreur en Simpson Composée]]
- [[#XIV Calcul des Paramètres]]
- [[#XV Résolution pour n]]

</div>
---
<div class="exercice-container"> <div class="exercice-header"> <div class="exercice-title">📊 Exercice 1 : Interpolation de Lagrange pour un gaz en thermodynamique</div> </div> <div class="exercice-content"> <div class="section"> <div class="section-title">I. Données de l'expérience</div> Les résultats expérimentaux fournis sont les suivants :

|Pression (P) [kPa]|Volume spécifique (Vg) [m³/kg]|
|---|---|
|308.6|0.055309|
|362.6|0.047485|
|423.3|0.040914|
|491.4|0.035413|

Nous allons construire le polynôme d'interpolation de Lagrange P(x) qui relie la pression P au volume spécifique Vg.

</div> <div class="section"> <div class="section-title">II. Méthode : Interpolation de Lagrange</div> Le polynôme d'interpolation de Lagrange pour un ensemble de points (xi, yi) est donné par : <div class="math-block math display" >P(x) = \sum_{i=0}^n y_i L_i(x)</div>

où Li(x) est le polynôme de base de Lagrange, défini par :

<div class="math-block math display"> L_i(x) = \prod_{j=0, j≠i}^n \frac{x - x_j}{x_i - x_j} </div> </div> <div class="section"> <div class="section-title">III. Calcul des polynômes de base de Lagrange</div> Nous avons quatre points, donc le polynôme d'interpolation sera de degré 3. Les polynômes de base sont calculés comme suit : <div class="math-block math display"> L_0(x) = \frac{(x - 362.6)(x - 423.3)(x - 491.4)}{(-54)(-114.7)(-182.8)} </div>
<div class="math-block math display">
L_1(x) = \frac{(x - 308.6)(x - 423.3)(x - 491.4)}{(54)(-60.7)(-128.8)}
</div>
<div class="math-block math display">
L_2(x) = \frac{(x - 308.6)(x - 362.6)(x - 491.4)}{(114.7)(60.7)(-68.1)}
</div>
<div class="math-block math display">
L_3(x) = \frac{(x - 308.6)(x - 362.6)(x - 423.3)}{(182.8)(128.8)(68.1)}
</div>
</div> <div class="section"> <div class="section-title">IV. Calcul du polynôme final</div> En multipliant chaque Li(x) par le volume spécifique correspondant Vg(xi) et en les sommant, nous obtenons : <div class="math-block math display"> P(x) = 0.055309L_0(x) + 0.047485L_1(x) + 0.040914L_2(x) + 0.035413L_3(x)</div>
<div class="math-block math display">
P(x) = -5.8031 × 10^{-10} x^3 + 9.5455 × 10^{-7} x^2 - 5.8908 × 10^{-4} x + 0.1632

</div> 
</div> <div class="section"> <div class="section-title">V. Approximation du volume spécifique pour P = 400 kPa</div> En utilisant le polynôme obtenu, nous calculons l'approximation de Vg pour une pression de 400 kPa : <div class="math-block math display"> V_g(400) ≈ 0.043156 \text{ m}^3/\text{kg} </div>

Le polynôme obtenu permet d'estimer le volume spécifique du gaz pour toute pression comprise entre 308.6 kPa et 491.4 kPa. Cette méthode d'interpolation est utile pour approximer des valeurs expérimentales et éviter des mesures supplémentaires coûteuses. Ce modèle peut également être utilisé pour extrapoler des valeurs en dehors de cette plage, bien que la précision ne soit pas garantie au-delà des points expérimentaux donnés.

</div> </div> </div>
---

<div class="exercice-container">
<div class="exercice-header">
<div class="exercice-title">📈 Exercice 2 : Approximation de la Vitesse et de l'Accélération</div>
</div>
<div class="exercice-content">

<div class="section">
 L'objectif est d'approximer la vitesse et l'accélération d'une voiture en utilisant une méthode numérique d'ordre deux. La loi horaire du mouvement est donnée par :

<div class="math-block math display">
x(t) = 35e^{2t}
</div>

où t est le temps en heures et x(t) est la distance parcourue en kilomètres.
</div>

<div class="section">
<div class="section-title">VI. Méthodes numériques</div>

<div class="subsection">
<div class="subsection-title">1. Approximation de la vitesse</div>
La vitesse est la dérivée première de x(t) :
<div class="math-block math display">
v(t) = x'(t)
</div>

Une approximation d'ordre 2 de cette dérivée est donnée par la méthode des différences finies centrées :
<div class="math-block math display">
v_{approx}(t) ≈ \frac{x(t + h) - x(t - h)}{2h}
</div>
</div>

<div class="subsection">
<div class="subsection-title">2. Approximation de l'accélération</div>
L'accélération est la dérivée seconde de x(t) :
<div class="math-block math display">
a(t) = x''(t)
</div>

Une approximation d'ordre 2 de cette dérivée est donnée par :
<div class="math-block math display">
a_{approx}(t) ≈ \frac{x(t + h) - 2x(t) + x(t - h)}{h^2}
</div>
</div>
</div>

<div class="section">
<div class="section-title">VII. Calculs</div>
Nous appliquons ces formules à t = 1 heure et h = 0.1.

<div class="subsection">
<div class="subsection-title">1. Calcul des valeurs de x(t)</div>
Nous calculons x(1 + h), x(1) et x(1 - h) :
<div class="math-block math display">
x(1.1) = 35e^{2(1.1)} = 315.87
x(1) = 35e^{2(1)} = 258.61
x(0.9) = 35e^{2(0.9)} = 211.73
</div>
</div>

<div class="subsection">
<div class="subsection-title">2. Calcul de la vitesse approximée</div>
<div class="math-block math display">
v_{approx}(1) = \frac{x(1.1) - x(0.9)}{2h} = \frac{315.87 - 211.73}{2 × 0.1} = 520.7 \text{ km/h}
</div>
</div>

<div class="subsection">
<div class="subsection-title">3. Calcul de l'accélération approximée</div>
<div class="math-block math display">
a_{approx}(1) = \frac{x(1.1) - 2x(1) + x(0.9)}{h^2} = \frac{315.87 - 2(258.61) + 211.73}{(0.1)^2} = 1038 \text{ km/h}^2
</div>
</div>
</div>

<div class="section">
<div class="section-title">VIII. Calcul des valeurs exactes</div>
La dérivée exacte de x(t) donne la vitesse :
<div class="math-block math display">
v_{exact}(t) = 70e^{2t}
</div>

Pour t = 1 :
<div class="math-block math display">
v_{exact}(1) = 70e^{2(1)} = 517.23 \text{ km/h}
</div>

La dérivée seconde donne l'accélération exacte :
<div class="math-block math display">
a_{exact}(t) = 140e^{2t}
</div>

Pour t = 1 :
<div class="math-block math display">
a_{exact}(1) = 140e^{2(1)} = 1034.47 \text{ km/h}^2
</div>
</div>

<div class="section">
<div class="section-title">IX. Comparaison des résultats</div>

|                      | Valeur Approximée | Valeur Exacte |
| -------------------- | ----------------- | ------------- |
| Vitesse (km/h)       | 520.7             | 517.23        |
| Accélération (km/h²) | 1038              | 1034.47       |

L'erreur relative de l'approximation est très faible, ce qui montre l'efficacité des différences finies centrées.

Nous avons utilisé la méthode des différences finies centrées pour approximer la vitesse et l'accélération d'un véhicule. Les résultats sont très proches des valeurs exactes, montrant que cette méthode est précise pour une fonction exponentielle.
</div>

</div>
</div>
---

<div class="exercice-container">
<div class="exercice-header">
<div class="exercice-title">🧮 Exercice 3 : Méthodes d'Intégration Numérique</div>
</div>
<div class="exercice-content">

<div class="section">
L'objectif est de calculer des valeurs approchées de trois intégrales définies en utilisant différentes méthodes d'intégration numérique :

- Méthode des points milieux pour 
<div class="math-block math display">
I = \int_0^{\pi/2} \sin(x^2) dx
</div> 
avec n = 5

- Méthode des trapèzes pour 
<div class="math-block math display">
I_1 = \int_0^1 \frac{1}{\sqrt{x^2 + 1}} dx
</div> 
avec n = 4

- Méthode de Simpson composée pour 
<div class="math-block math display">
I_2 = \int_0^1 e^{x^2} dx
</div> 
avec n = 6
</div>

<div class="section">
<div class="section-title">X. Méthode des Points Milieux</div>

La méthode des points milieux consiste à approximer une intégrale définie en subdivisant l'intervalle [a, b] en n sous-intervalles de largeur égale :

<div class="math-block math display">
h = \frac{b - a}{n}
</div>

Au lieu d'évaluer la fonction aux extrémités des sous-intervalles, on l'évalue en **leur point milieu** :

<div class="math-block math display">
m_i = \frac{x_i + x_{i+1}}{2}
</div>

Nous avons les extrémités des sous-intervalles définies par :
<div class="math-block math display">
x_i = a + ih, x_{i+1} = a + (i + 1)h
</div>

En substituant ces valeurs dans l'expression du point milieu :

<div class="math-block math display">
m_i = \frac{a + ih + a + (i + 1)h}{2} = \frac{2a + 2ih + h}{2} = a + ih + \frac{h}{2} = a + (i + \frac{1}{2})h
</div>

L'intégrale sur un sous-intervalle [xi, xi+1] est alors approximée par :

<div class="math-block math display">
\int_{x_i}^{x_{i+1}} f(x)dx ≈ hf(m_i)
</div>

En sommant sur tous les sous-intervalles, on obtient la formule de la méthode des points milieux :

<div class="math-block math display">
\int_a^b f(x)dx ≈ h\sum_{i=0}^{n-1} f(m_i)
</div>

Pour notre intégrale :
- a = 0, b = π/2 (bornes de l'intégrale)
- n = 5 (nombre de sous-intervalles)
- La largeur des sous-intervalles : 
<div class="math-block math display">
h = \frac{b - a}{n} = \frac{\pi/2 - 0}{5} = \frac{\pi}{10}
</div>

Les points milieux sont :
<div class="math-block math display">
m_0 = \frac{\pi}{20}
m_1 = \frac{3\pi}{20}
m_2 = \frac{5\pi}{20}
m_3 = \frac{7\pi}{20}
m_4 = \frac{9\pi}{20}
</div>

L'approximation finale est :
<div class="math-block math display">
I ≈ 0.8383
</div>
</div>

<div class="section">
<div class="section-title">XI. Méthode des Trapèzes</div>

Pour l'intégrale :
<div class="math-block math display">
I_1 = \int_0^1 \frac{1}{\sqrt{x^2 + 1}} dx
</div>

La formule d'approximation est :
<div class="math-block math display">
\int_a^b f(x)dx ≈ \frac{b-a}{2n}[f(a) + 2\sum_{i=1}^{n-1}f(x_i) + f(b)]
</div>

Paramètres :
- a = 0, b = 1
- n = 4
- h = 0.25

Évaluation aux points :
<div class="math-block math display">
f(x_0) = 1.0000
f(x_1) = 0.9701
f(x_2) = 0.8944
f(x_3) = 0.8000
f(x_4) = 0.7071
</div>

L'approximation finale est :
<div class="math-block math display">
I_1 ≈ 0.8795
</div>
</div>

<div class="section">
<div class="section-title">XII. Méthode de Simpson Composée</div>

Pour l'intégrale :
<div class="math-block math display">
I_2 = \int_0^1 e^{x^2} dx
</div>

La formule de Simpson composée :
<div class="math-block math display">
\int_a^b f(x)dx ≈ \frac{b-a}{3n}[f(a) + 2\sum_{i=1}^{n-1}f(x_{2i}) + 4\sum_{i=0}^{n-1}f(x_{2i+1}) + f(b)]
</div>

Paramètres :
- a = 0, b = 1
- n = 6
- h = 1/12

Après évaluation aux points et calculs :
<div class="math-block math display">
I_2 ≈ 2.9252
</div>

Cette méthode offre généralement une meilleure précision que les deux précédentes pour un même nombre de points d'évaluation.
</div>

</div>
</div>
---

<div class="exercice-container">
<div class="exercice-header">
<div class="exercice-title">📐 Exercice 4 : Détermination de n pour la Méthode de Simpson</div>
</div>
<div class="exercice-content">

<div class="section">
L'objectif est de déterminer le nombre de subdivisions n pour évaluer l'intégrale suivante avec une précision de 0.251 × 10^-3 en utilisant la méthode de Simpson composée :

<div class="math-block math display">
I = \int_{-\pi}^{\pi} \cos(x) dx
</div>
</div>

<div class="section">
<div class="section-title">XIII. Formule de l'Erreur en Simpson Composée</div>

L'erreur de la méthode de Simpson composée est donnée par :

<div class="math-block math display">
E = \frac{(b - a)h^4}{180} \times \max_{x\in[a,b]}|f^{(4)}(x)|
</div>

Nous devons trouver n tel que :

<div class="math-block math display">
|E| \leq 0.251 \times 10^{-3}
</div>
</div>

<div class="section">
<div class="section-title">XIV. Calcul des Paramètres</div>

Nous avons :
- a = -π, b = π
- Le pas h est défini par :
<div class="math-block math display">
h = \frac{b-a}{n} = \frac{2\pi}{n}
</div>

- La quatrième dérivée de f(x) = cos(x) :
<div class="math-block math display">
f^{(4)}(x) = \cos(x)
</div>

- La valeur maximale de |f^(4)(x)| sur [-π, π] est :
<div class="math-block math display">
\max |f^{(4)}(x)| = 1
</div>
</div>

<div class="section">
<div class="section-title">XV. Résolution pour n</div>

Substituons ces valeurs dans la formule de l'erreur :

<div class="math-block math display">
\frac{2\pi h^4}{180} \times 1 \leq 0.251 \times 10^{-3}
</div>

En remplaçant h = 2π/n, nous obtenons :

<div class="math-block math display">
\frac{2\pi}{180} \times (\frac{2\pi}{n})^4 \leq 0.251 \times 10^{-3}
</div>

En résolvant pour n, nous trouvons :

<div class="math-block math display">
n \approx 21.58
</div>

Comme n doit être un nombre pair pour la méthode de Simpson, nous prenons :

<div class="math-block math display">
n = 22
</div>

Nous avons déterminé que le nombre de subdivisions nécessaire pour obtenir une précision de 0.251 × 10^-3 en utilisant la méthode de Simpson composée est n = 22. Cette valeur garantit une erreur inférieure au seuil spécifié.
</div>

</div>
</div>


