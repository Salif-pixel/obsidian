

---
```java
public static void somme_lignes(int [][] C,int i,int j,int nl)  
{  
    if (i>nl-1)  
        return;  
    else  
    {  
        int somme=0;  
        for (int k=0;k<C[i].length;k++)  
            somme=somme+C[i][k];  
        System.out.println("Somme de la ligne "+i+" vaut:"+somme);  
        somme_lignes(C,i+1,0,nl);  
    }  
}

public int compte1f(Noeud noeud)  
{  
    if (noeud==null)  
        return 0;  
    else if (noeud.gauche==null && noeud.droit==null)  
        return 0;  
    else if (noeud.gauche!=null && noeud.droit==null)  
        return 1+compte1f(noeud.gauche);  
    else if (noeud.gauche==null && noeud.droit!=null)  
        return 1+compte1f(noeud.droit);  
    else  
        return 0+compte1f(noeud.gauche)+compte1f(noeud.droit);  
}  

public String afficher1f(Noeud noeud){  
    if (noeud==null)  
        return " ";  
    else if (noeud.gauche==null && noeud.droit==null)  
        return " ";  
    else if (noeud.gauche!=null && noeud.droit==null)  
        return " "+noeud.data+afficher1f(noeud.gauche);  
     else if (noeud.gauche==null && noeud.droit!=null)  
        return " "+noeud.data+afficher1f(noeud.droit);  
    else  
        return " "+afficher1f(noeud.gauche)+afficher1f(noeud.droit);  
}

public Boolean isEulerian() {  
    int[] degres = degresDesSommets();  
    int countDegresImpairs = 0;  
  
    for (int i = 0; i < degres.length; i++) {  
        if (degres[i] % 2 != 0)  
            countDegresImpairs++;  
    }  
    if (countDegresImpairs == 0)  
        return true;  
    else if (countDegresImpairs == 2)  
        return true;  
    else  
        return false;  
}  

public int[] degresDesSommets() {  
    int[] degres = new int[adj.length];  
    for (int i = 0; i < adj.length; i++) {  
        int degre = 0;  
        for (int j = 0; j < adj[i].length; j++) {  
            if (adj[i][j] == 1) { // 1 signifie une arête entre i et j  
                degre++;  
            }  
        }  
        degres[i] = degre;  
    }  
    return degres;  
}
```