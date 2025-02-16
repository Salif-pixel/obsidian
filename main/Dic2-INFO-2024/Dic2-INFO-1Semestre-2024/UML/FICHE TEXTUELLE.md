
---
## 1. Suivi du Budget

**Objectif :**  
Permettre à l'utilisateur de consulter l'état global du budget, c'est-à-dire les montants alloués, dépensés et restants, éventuellement par catégorie.

**Acteurs principaux :**

- Administrateur
- Responsable budgétaire

**Préconditions :**

- L'utilisateur est authentifié.
- Un budget global (ou plusieurs budgets) a été défini dans le système.
- Des dépenses ont été enregistrées.

**Flux principal :**

1. **Connexion et navigation :** L'utilisateur se connecte et sélectionne la section "Suivi du budget".
2. **Affichage des données :** Le système affiche les montants alloués, les dépenses cumulées et le solde restant.
3. **Filtrage/tri :** L'utilisateur peut filtrer ou trier les informations par catégorie, période, etc.
4. **Mise à jour en temps réel :** Les chiffres se mettent à jour automatiquement à chaque nouvelle dépense ou modification.

**Flux alternatif :**

- **Pas de budget défini :** Si aucun budget n'est enregistré, le système affiche un message invitant à créer un budget.

**Postconditions :**

- L'utilisateur a une vision claire et à jour de l’état budgétaire.

---

## 2. Catégorisation des Dépenses

**Objectif :**  
Permettre de classer chaque dépense dans une catégorie prédéfinie (ex. équipements, fonctionnement) afin de faciliter l’analyse et la génération de rapports.

**Acteurs principaux :**

- Administrateur
- Utilisateur (avec droits de saisie)

**Préconditions :**

- L'utilisateur est authentifié.
- Une liste de catégories existe ou peut être créée/modifiée.

**Flux principal :**

1. **Accès à la gestion des catégories :** L'utilisateur navigue vers la section "Catégorisation des dépenses".
2. **Consultation et modification :**
    - Visualisation des catégories existantes.
    - Possibilité d'ajouter, de modifier ou de supprimer une catégorie.
3. **Saisie d'une dépense :** Lors de l'enregistrement d'une dépense, l'utilisateur sélectionne la catégorie correspondante dans une liste déroulante.

**Flux alternatif :**

- **Catégorie manquante :** Si la catégorie souhaitée n'existe pas lors de la saisie, le système peut proposer de la créer instantanément.

**Postconditions :**

- Chaque dépense est correctement associée à une catégorie, facilitant ainsi les analyses ultérieures.

---

## 3. Saisie et Validation d’une Dépense

**Objectif :**  
Permettre à l'utilisateur de saisir une dépense, de la soumettre et, si nécessaire, de la faire valider par un administrateur.

**Acteurs principaux :**

- Utilisateur (pour la saisie)
- Administrateur (pour la validation, si applicable)

**Préconditions :**

- L'utilisateur est authentifié.
- Un budget et des catégories de dépenses existent dans le système.

**Flux principal :**

4. **Accès au formulaire :** L'utilisateur clique sur "Nouvelle dépense" et remplit le formulaire avec les informations nécessaires (montant, date, description, catégorie, etc.).
5. **Vérification des données :** Le système vérifie la cohérence des informations saisies (ex. montant positif, date valide).
6. **Soumission de la dépense :**
    - **Validation automatique :** Si le processus est configuré pour une validation automatique, la dépense est enregistrée et le budget est mis à jour.
    - **Validation manuelle :** Si une validation manuelle est requise, une notification est envoyée à l'administrateur qui approuve ou rejette la dépense.
7. **Mise à jour du budget :** En cas d'approbation, le montant dépensé est ajouté au total des dépenses, et le solde du budget est recalculé.

**Flux alternatif :**

- **Erreur de saisie :** Si des erreurs sont détectées (ex. champ obligatoire manquant), le système affiche un message d'erreur demandant une correction.
- **Sauvegarde en brouillon :** L'utilisateur peut avoir la possibilité d’enregistrer la dépense en brouillon avant de la soumettre définitivement.

**Postconditions :**

- La dépense est enregistrée dans le système et intégrée au suivi du budget une fois validée.

---

## 4. Génération Automatique de Rapports Financiers

**Objectif :**  
Permettre la création de rapports financiers basés sur les données de budget et de dépenses, pour une analyse rapide et une présentation sous forme de tableau ou exportable en PDF/CSV.

**Acteurs principaux :**

- Administrateur
- Utilisateur (selon les droits)

**Préconditions :**

- Des données de budget et de dépenses sont présentes dans le système.

**Flux principal :**

8. **Accès à la section rapports :** L'utilisateur navigue vers "Rapports financiers".
9. **Sélection du type de rapport :** L'utilisateur choisit le format ou le type de rapport (global, par catégorie, par période, etc.).
10. **Génération des rapports :**
    - Le système agrège les données pertinentes.
    - Le rapport est généré automatiquement et affiché à l’écran.
11. **Exportation et impression :** L'utilisateur peut exporter le rapport (ex. en PDF ou CSV) ou l’imprimer directement.

**Flux alternatif :**

- **Données insuffisantes :** Si aucune dépense ou budget n’est enregistré pour la période choisie, le système informe l'utilisateur et propose de modifier les critères.

**Postconditions :**

- Un rapport financier détaillé et exportable est généré, fournissant une analyse claire de l’état budgétaire.

---

## 5. Consultation de l’Historique des Dépenses

**Objectif :**  
Permettre à l'utilisateur de consulter l'ensemble des dépenses enregistrées, ainsi que l’historique des modifications et validations.

**Acteurs principaux :**

- Administrateur
- Utilisateur (avec accès à l’historique)

**Préconditions :**

- L'utilisateur est authentifié.
- Un historique de toutes les dépenses et modifications est disponible dans la base de données.

**Flux principal :**

12. **Accès à l’historique :** L'utilisateur sélectionne la section "Historique des dépenses".
13. **Affichage des dépenses :** Le système liste toutes les dépenses avec leurs détails (date, montant, catégorie, statut, etc.).
14. **Filtrage et tri :**
    - L'utilisateur peut filtrer par période, catégorie, ou statut (validée, en attente, rejetée, etc.).
    - Il peut trier les résultats selon différents critères.
15. **Consultation détaillée :** En cliquant sur une dépense, l'utilisateur peut voir les détails complets et l’historique des modifications (qui a validé, quand, etc.).

**Flux alternatif :**

- **Aucune donnée :** Si aucune dépense n'est enregistrée, le système affiche un message informatif.

**Postconditions :**

- L'utilisateur peut consulter et analyser l’historique complet des dépenses pour assurer une traçabilité et une transparence totale.