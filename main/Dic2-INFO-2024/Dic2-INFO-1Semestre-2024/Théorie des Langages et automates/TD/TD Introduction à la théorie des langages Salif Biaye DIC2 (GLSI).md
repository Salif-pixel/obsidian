
---
# TD1 
## Exercice1: Alphabets et mots
- Comptons le nombre d'occurrences des lettres a et b dans les mots suivants

> `aabg,jdd,titi,babc,a^3cbbca`.
>`|m|a` dans `aabg` = 2
>`|m|a` dans `jdd` = 0
>`|m|a` dans `titi` = 0
>`|m|a` dans `babc` = 1
>`|m|a` dans `a^3cbbca` = 4
>`|m|b` dans `aabg` = 1
>`|m|b` dans `jdd` = 0
>`|m|b` dans `titi` = 0
>`|m|b` dans `babc` = 2
>`|m|b` dans `a^3cbbca` = 2

- Donnons l'ensemble des couples (`u,v`) tels que `uv =abaac`

> `u=a, v=baac  → uv=abaac`
>`u=ab , v=aac  → uv=abaac `
>`u=aba , v=ac  → uv=abaac`
>`u=abaa, v=c  → uv=abaac`
>` u=abaac , v=ε → uv=abaac`

- Déterminons les facteurs , les préfixes et les suffixes du mot u = `abac`

1. Les facteurs

>`"ε"`
>` "a"`
>`"b"`
>`"c"`
>`"ab"`
>`"ba"`
>`"ac"`
>`"aba"`
>`"bac"`
>`"abac"`
2. Les préfixes

> `"ε"`
>`"a"`
>` "ab"`
>`"aba"`
>`"abac"`
3. Les suffixes

> `"ε"`
>`"c"`
>` "ac"`
>`"bac"`
>`"abac"`

**Soient les alphabets suivants :**

- $$Σ1=\Sigma_1 = \{a, b\}$$
- $$Σ2=\Sigma_1 = \{d,e,f\}$$
- $$Σ3=\Sigma_1 = \{b, cd\}$$
- Donnez les alphabets suivants ainsi que quelques mots qu’ils peuvent générer par la fermeture de Kleene.


1. $$Σ_1^1= \{a, b\}$$
2.  $$Σ_1^2= \{aa, ab,ba,bb\}$$
3. $$Σ_2^3= \{ddd, eee,fff,dde,ddf,def,ded,fed,fef,eed,eef,edf,efd,ffe,ffd,fed,fde,...\}$$
4. $$Σ_2^1 U Σ_3^2= \{df, e,bb,bcd,cdb,cdcd\}$$
5. $$(Σ_1 U Σ_2)^2= \{aa,ab,ba,bb,ad,ae,af,bd,be,bf,ea,da,fa,db,eb,fb,ff,dd,ee,fe,ef,fd,df,de,ed\}$$

---


## Exercice 2 : Langages

Soit l’alphabet Σ={a,b} Donnez une description des langages suivants et quelques exemples de mots.

### Langages donnés :

1. $$L1=Σ^n,n∈N^*$$
2. L2=`m∈Σ^∗ avec ∣m∣_a=∣m∣_b`
3. L3=`a^ib^j avec 0≤i≤j`
4. L4=`a^n,b^m avec (m,n) ∈ N^2`
5. $$L5={a,ba}, / alors que représente L^*$$
6. $$L6={a^n,b | n >=0}, / alors que représente L^*$$



1. L1 : L'ensemble des mots non vide
    
2. L2: L'ensemble des mots dont le nombre de symbole a soit égale au nombre de symbole de b
    
3. L3:  L'ensemble  des mots contenant i a suivis de j b, avec i≤j avec i et j >=0
    
4. L4:  L'ensemble  des mots contenant n a suivis de m b, avec n et m >=0
    
5. L5:  L* représente la fermeture de Kleene du langage L5
    
6. L6 : L* représente la fermeture de Kleene du langage L6
    



---

## Exercice 3 : Operations sur les langages

1. Soit l'alphabet :  
`    Σ={a,b,c}`
    
2. Les langages définis :
    
    `- L1={ab,ba}
    `- L2={c,cc}`
    `- L3={ac}``

---

### Question 1 : Calcul des opérations sur L1,L2,L3

#### a) L1L2


`L1​L2​={abc,abcc,bac,bacc}`

#### b) L1L2L3



`L1L2L3={abcac,abccac,bacac,baccac}`

#### c) L_1^2



`L_1^2={abab,abba,baab,baba}`

---


**Langages donnés :**

L1 = {abb, b, a}  
L2 = {ba, baa, a}

**1. (L1)³ ∩ L2**

Calcul de (L1)² :  
(L1)² = {abb, b, a}{abb, b, a}  
= {abbabb, abbb, abba, babb, bb, ba, aabb, ab, aa}

Calcul de (L1)³ :  
(L1)³ = {abbabb, abbb, abba, babb, bb, ba, aabb, ab, aa}{abb, b, a}  
= {abbabbabb, abbabbb, abbabba, abbbabb, abbbb, abbba, abbaabb, abbab, abbaa, babbabb, babbb, babba, bbabb, bbb, bba, baabb, bab, baa, ababb, aabbb, aabba, ababb, abb, aba, aaabb, aab, aaa}

**2. (L1)³ ∩ L2 = {baa}**

**3. Calcul de (L1 ∪ L2)**

L1 ∪ L2 = {abb, b, a} ∪ {ba, baa, a}  
= {abb, b, a, ba, baa}

Calcul de (L1 ∪ L2)² :  
(L1 ∪ L2)² = {abb, b, a, ba, baa}{abb, b, a, ba, baa}  
= {abbabb, abbb, abba, abbba, abbbaa, babb, bb, ba, bba, bbaa, aabb, ab, aa, aba, abaa, baabb, bab, baa, baba, babaa, baaabb, baab, baaa, bba, baaba, baabaa}

**4. Calcul de (L1 ∪ L2)² ⋅ L2**

(L1 ∪ L2)² ⋅ L2 = {abbabb, abbb, abba, abbba, abbbaa, babb, bb, ba, bba, bbaa, aabb, ab, aa, aba, abaa, baabb, bab, baa, baba, babaa, baaabb, baab, baaa, bba, baaba, baabaa} ⋅ {ba, baa, a}  
= {abbabbba, abbabbbaa, abbabba, abbbba, abbbbaa, abbba, abbaba, abbbabaa, abbaa, abbbaba, abbbabaa, abbbaa...}


---
## Exercice 4 : Reconnaisseur

 - Dans quel état se trouve R Apres la lecture des mots `a, ab, abb, abba `
 1. `a`
	
| État | Entrée | État suivant |
| ---- | ------ | ------------ |
| 0    | a      | 1            |

2. `ab`

| État | Entrée | État suivant |
| ---- | ------ | ------------ |
| 0    | a      | 1            |
| 1    | b      | 2            |
3. `abb`

| État | Entrée | État suivant |
| ---- | ------ | ------------ |
| 0    | a      | 1            |
| 1    | b      | 2            |
| 2    | b      | 2            |
4. `abba`

| État | Entrée | État suivant |
| ---- | ------ | ------------ |
| 0    | a      | 1            |
| 1    | b      | 2            |
| 2    | b      | 2            |
| 2    | a      | 2            |
- Que se passe t-il quand on donne le mot `aab` à lire à R

	on remarque qu'a partir de l'état 1 il ne pourra plus se déplacer pour lire un prochain symbole a car il n'y a pas de chemin
	
- les mots aba^2 b,a^2ba^2 b,ab^4 et b^3 a^2 sont-ils reconnus par R ?

	aba^2 b et ab^4 seront reconnus
	a^2ba^2 b et a^2 ne seront pas reconnus

---
## Exercice 5: Grammaire de réécriture

Soit la grammaire formelle G=({S,R},{a,b},P,S)G = (\{S, R\}, \{a, b\}, P, S)G=({S,R},{a,b},P,S), où l'ensemble des règles de production PPP est :

1. `S→aS`
2. `S→bR`
3. `S→b`
4. `R→aR`
5. `R→bS`



### Question 1 : Montrer que le mot abb est généré par G

Pour générer `abb `:

1. `S→aS`  : on génère a, reste S.
2. `S→bR`  : on génère b, reste R.
3. ` R→bS`: on génère b, reste R.
4. `S→b` : on génère b, il ne reste plus rien.

Ainsi, le mot abbb est obtenu.



### Question 2 : Montrer que le mot abb n'est pas généré par G

1. `S→aS`  : on génère a, reste S.
2. `S→bR`  : on génère b, reste R.
3. ` R→bS`: on génère b, reste R.
et donc on aura `abbR` or R ne peut pas donner `ε` donc `abb` ne peut être  généré par G


# TD2

---

## Exercice 1 :
Pour chaque affirmation, dire si elle est vraie ou fausse puis justifier :

1) Tout langage régulier est infini.  
**Faux** : ∅ est fini et ∅ est un langage régulier.

2) Il y a une infinité de langages réguliers.  
**Vrai** : on peut avoir une infinité d’E.R et chaque E.R désigne un langage régulier.

3) L’union de 2 langages reconnaissables est reconnaissable.  
**Vrai** : les langages reconnaissables sont clos par l’union.

4) L’intersection de deux langages reconnaissables est un langage reconnaissable.  
**Vrai** : car les langages reconnaissables sont clos par l’intersection.

---

## Exercice 2 :
Ces E.R contiennent-elles le mot vide ?

1. (a + b)a\* b(a + b(b + ab)\*)\*  
   **⇔ b donc ne contient pas ∈.**

2. (a + b)(aa\* + bb\*a)\*  
   **⇔ a + b ne contient pas le mot vide ∈.**

3. (a + c)(a + b)(1 + c)(1 + d)(∈ + f)  
   **⇔ ne contient pas le mot vide.**

4. (a + (b + (c + d)\*))\*  
   **⇔ ∈ donc contient le mot vide.**

---

## Exercice 3 :
Donnons tous les mots de longueur 0, 1, 2, 3 et 4 dans les langages réguliers suivants :

1. (a.b + ba)\*  
   - L⁰ = {∈}  
   - L¹ = {a, b}  
   - L² = {aa, ba}  
   - L³ = {aaa, aba, baa}  
   - L⁴ = {abaa, baba, aaaa, aaba, baaa}  

2.  a(aa + b(ab)\*a)\*a  
   - L⁰ = ∅  
   - L¹ = ∅  
   - L² = {aa}  
   - L³ = ∅  
   - L⁴ = {aaaa, abaa}  

---

## Exercice 4 :
Soit A = {a, b}. Donnez la description des langages donnés par les expressions relationnelles :

1. A\* 
   {m ∈ {a, b}∗ / m représente l’ensemble de tous les mots .}

2. **AA**  
   {m ∈ {a, b}∗ / m représente l’ensemble de tous les mots de longueur 2.}

3. **(E + A)(E + A)**  
   {m ∈ {a, b}∗ / |m| ≤ 2, tous les mots de longueur au plus 2 sur {a, b}.}

4. (AA)\* 
   {m ∈ {a, b}∗ / m représente l’ensemble de mots de longueur paire sur A = {a, b}.}

5. aA\* 
   {m ∈ {a, b}∗ / m représente l’ensemble de mots commençant par a.}

6. A\* a  
   {m ∈ {a, b}∗ / m représente l’ensemble de mots terminant par a.}

7. A\* a A\*
   {m ∈ {a, b}∗ / m représente l’ensemble de mots contenant le mot a ou bien a est facteur.}

8. A\* abA\*  
   {m ∈ {a, b}∗ / m représente l’ensemble de mots où ab est le facteur du mot m.}

9. A\* aA\* bA\*
   L’ensemble de tous les mots sur l’alphabet {a, b} avec au moins une occurrence de a suivie par au moins une occurrence de b.

10. **(b + ab)(a + E)**  
    {m ∈ {a, b}∗ / m représente l’ensemble de mots se terminant par a.}

11. a\* + b\* 
    {m ∈ {a, b}∗ / m représente l’ensemble de mots contenant 0 ou plusieurs a ou bien 0 ou plusieurs b.}

12. (aa + b)\* 
	m ∈ {a, b}∗ / m représente l'ensemble des mots formés de **zéro ou plusieurs** répétitions de "aa" et de "b"

13. (ab\* a + b)
	{m ∈ {a, b}∗ / m est composé de zéro ou plusieurs répétitions de une occurrence de "a", suivie de zéro ou plusieurs "b", puis un autre "a", ou simplement une occurrence de "b".}

14. (ab)\*
    {m ∈ {a, b}∗ / m représente l’ensemble des mots contenant 0 ou plusieurs ab sur A = {a, b}.}

15. a\* + bc\* d
    {m ∈ {a, b}∗ / m représente l’ensemble de mots contenant uniquement des "a" (y compris la chaîne vide), ou contenant un "b", suivi de zéro ou plusieurs "c", et se terminant par un "d".}


## Exercice 5

1. le langage des mots qui entre deux occurrences de la lettre a ont un nombre pair de b

	b\* +(a(bb)*a)*+b\*
2. Le langage des mots tels que toutes les éventuelles occurrences de a precedent toute les éventuelles occurrences de b
	a\* b\*

## Exercice 6
### Le langage L(E) :

Le langage L(E), qui est l'ensemble des chaînes acceptées par l'expression régulière E, est donc constitué de toutes les chaînes qui :

- Se terminent par un "c",
- Et qui avant ce "c" peuvent contenir n'importe quelle combinaison de "a" et "b", ou rien du tout (c'est-à-dire la chaîne vide).

Ainsi, le langage L(E) est formé des chaînes suivantes :

- "", "c", "ac", "bc", "abc", "bac", "aabbc", "abac", etc.

En résumé, L(E) est l'ensemble de toutes les chaînes qui se terminent par un "c", et qui avant ce "c" peuvent être composées de n'importe quel lettre entre   "a" et "b" ou epsilon.


["dd1","22lds","dk-2knd"]
[["dd1","22l,ds"],["dk-2knd"]]
[[["1dd1"],"22l,ds","dk-2knd"]]]