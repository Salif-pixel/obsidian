
---

# Processus
Une **instance** d'exécution d'un programme

---

## Ressources
- **Matérielles**
  - CPU
  - Périphériques
- **Logicielle**
  - Code
  - contexte
  - mémoire

## Mode d'exécution
### Mode utilisateur VS Mode Noyau

## Identification des processus

`PID process identifier` c'est un numéro unique qui vient a sa naissance il est coder  de la même manière qu'un entier non signe qui est 4 octets 0 ----> 2^32

`-start-kernel()` il va créer 
- un Processus 0
	- Initialiser les structures de données du noyau
	- Autoriser les interruptions
	- Créer un thread init (destiner a une tache spécifique)
	- Dormir (a son réveil il tue tout le monde)

`# init 0` entraine un arrêt brutal du système
	- il va créer d'autres thread de gestion:
		- Cache
		- Swap
		- autre
    - `exec(-)`
	    - INIT de PID =1 

## Informations sur les processus
commande `ps` avec d'autres options `-aux` par exemple il donne une cartographie du système a un instant t
il y a une versions `top` elle donne l'état du système a un temps réel
# Processus et Identification

## Fonctions et Processus

- **`pid_t getpid(void)`** : Fonction qui retourne l'identifiant du processus courant.
- **`pid_t getppid(void)`** : Fonction qui retourne l'identifiant du processus parent.

---

### Exemple de Processus

1. **Processus P1**
   - `getpid();` → `PID(P1)`
   - **Créer un processus** → Nouveau processus P2
   - `PPID(P2) = PID(P1)`

2. **Processus P2**
   - `getpid();` → `PID(P2)`
   - `getppid();` → `PID(P1)`

---

### Résumé des Relations entre Processus

- **P1** est le processus parent de **P2**.
- **P2** peut obtenir le PID de **P1** en utilisant `getppid()`.

## Proprietaire Réel vs Proprietaire effective

## Creation de processus

- P1
			- fork();  