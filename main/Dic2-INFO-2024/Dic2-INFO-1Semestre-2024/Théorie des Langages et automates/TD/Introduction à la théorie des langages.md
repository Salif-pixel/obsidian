
---
# Exercice1:
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
- Les facteurs
>` "a"`
>`"b"`
>`"c"`
>`"ab"`
>`"ba"`
>`"ac"`
>`"aba"`
>`"bac"`
>`"abac"`
- Les préfixes
> `""`
>`"a"`
>` "ab"`
>`"aba"`
>`"abac"`
- Les suffixes
> `""`
>`"c"`
>` "ac"`
>`"bac"`
>`"abac"`