# Senior Dev Assessment

# -- Odoo Functional (15 min)--

### Question 1:

Comment configurer un workflow dans Odoo pour gérer le processus de validation des factures dans une entreprise de services, en prenant en compte qu'une facture doit être validée par un responsable de département avant d'être envoyée au client ? Quels outils Odoo à utiliser pour cela et comment les configurer ?

### Question 2:

Comment gérer l'inventaire d'une entreprise ayant plusieurs entrepôts et des produits avec des dates de d'éxpiration ? Comment configurer Odoo pour s'assurer que les produits sont correctement stockés et suivis par numéro de lot et date d'éxpiration, et qu'une alerte est envoyée lorsque des produits arrivent à expiration ?

## Question 3:

Dans un scénario où une entreprise utilise Odoo pour gérer les ventes, comment configurer le système pour permettre à un vendeur de transformer un devis en commande sans changer les prix définis au préalable, tout en permettant une gestion flexible des remises sur certains articles du devis ? Quel impact cela aurait-il sur les reports de performance et les marges ?


# -- Odoo Technical (20 - 30 min)--

# Optimisation d'une Requête SQL Lente dans Odoo

## Contexte  
Tu travailles sur un module Odoo 16 qui gère les stocks. Une requête SQL personnalisée, exécutée dans une méthode `_compute_total_stock()`, met plusieurs secondes à s’exécuter sur une base de données contenant **5 millions de lignes** dans `stock_move`.

### Requête actuelle :
```sql
SELECT product_id, SUM(quantity_done) AS total_qty
FROM stock_move
WHERE state = 'done'
GROUP BY product_id;
```

Cette requête est utilisée pour calculer le stock total de chaque produit en fonction des mouvements validés.

### Problème :
Cette requête est lente, surtout quand elle est exécutée plusieurs fois sur une grande base de données.
L’impact est visible sur les performances des vues et des rapports.

### Tâche :
1- Identifier les causes potentielles du problème de performance.

2- Proposer et expliquer une optimisation.

2- Si possible, fournir une version optimisée de la requête SQL ou une alternative via Odoo ORM.



# Développement d'un Champ Calculé et d'un Bouton d'Action dans Odoo

## Contexte :
Votre entreprise gère des installations électriques à l'aide d'Odoo. Vous souhaitez implémenter une fonctionnalité permettant de calculer automatiquement le coût total des interventions d’un ticket Helpdesk, en fonction du temps passé par les techniciens et du taux horaire appliqué.

### Tâches Demandées :

1. Créer un champ calculé `total_cost` dans le modèle `helpdesk.ticket`.
   - Ce champ doit être calculé en fonction des valeurs des champs `time_spent` (temps total passé sur le ticket, en heures) et `hourly_rate` (taux horaire du technicien).
   - Le taux horaire doit être configurable au niveau du ticket, tout en héritant d’un taux par défaut défini sur l’employé du technicien.

2. Ajouter un bouton d’action "Facturer Intervention" sur les tickets Helpdesk.
   - Ce bouton doit générer une facture client (`account.move`) avec une ligne correspondant au coût total de l’intervention.
   - Si le ticket a déjà été facturé, le bouton doit être désactivé.

### Données disponibles :

- **helpdesk.ticket** :
  - `time_spent` (Float) : Temps total passé sur le ticket, en heures.
  - `hourly_rate` (Float) : Taux horaire du technicien, configurable.
  - `total_cost` (Float) : Champ à calculer.
  - `is_invoiced` (Boolean) : Indique si le ticket a été facturé.
  - `partner_id` (Many2one vers `res.partner`) : Client du ticket.

- **hr.employee** :
  - `default_hourly_rate` (Float) : Taux horaire par défaut du technicien.

- **account.move** :
  - Utilisé pour générer la facture client.

- **exemple du format du bouton dans le fichier xml**
```xml
<button name="XXX" type="object" string="XXX" class="oe_highlight" attrs="{XXX}"/>
```

# Développement d'un flux utilisateur web

## Context :
Tu travailles en tant que développeur Odoo et tu dois mettre en place un flux de formulaires en plusieurs étapes. Ces formulaires sont utilisés par des utilisateurs externes (non connectés à Odoo) pour soumettre des informations qui seront liées à un lead dans le CRM.

Ce flux doit respecter plusieurs contraintes :
1.	Suivi des étapes : L'utilisateur ne peut pas sauter d'étape sans avoir rempli les formulaires précédents.
2.	Validation des données : Les champs doivent être correctement remplis et validés pour éviter toute incohérence ou injection de données indésirables.
3.	Bonne structuration du code : La logique métier doit être placée dans le modèle et non dans le contrôleur pour assurer la cohérence du processus.
4.	Accès sécurisé sans connexion Odoo : L’utilisateur doit pouvoir remplir les formulaires sans être connecté à Odoo, mais les données doivent rester protégées et liées à son lead.

### Contrôler le flux utilisateur sur différentes étapes de formulaires

Q : Comment empêcher un utilisateur d’accéder à une étape ultérieure si les étapes précédentes ne sont pas complètes ?

Q : Comment gérer le stockage temporaire des données d’un formulaire avant validation finale ?

Q : Quelle solution proposerais-tu pour qu'un utilisateur ne puisse pas modifier un formulaire déjà validé ?

### Bonne pratique d’enregistrement des champs

Q : Comment éviter l’injection de données indésirables via un formulaire Odoo ?

### Séparation du code business et des contrôleurs

Q : Pourquoi est-il préférable de mettre une partie du code business dans le modèle plutôt que dans le contrôleur ?

Q : Comment organiser le code pour s’assurer que les règles métier s’appliquent quel que soit le point d’entrée dans le système ?

Q : Peux-tu donner un exemple où une règle métier mal placée dans un contrôleur pourrait poser problème ?

### Accès aux données sans authentification Odoo

Q : Comment permettre à un utilisateur d’accéder à un flux de formulaires lié à un lead sans être connecté à Odoo ?

Q : Quels sont les risques de sécurité à prendre en compte en exposant un formulaire accessible publiquement ?

### Gestion des pages web et leurs performances

Q : Comment optimiser les images pour améliorer la performance d’une page HTML ?

Q : Quels éléments HTML permettent d’améliorer le SEO et l’accessibilité d’une page ?

# Odoo et le framework html

Q : Quel framework html/css est intégré à Odoo, et quelles sont les principales classes CSS que l'on peut utiliser directement dans les vues Odoo ?

Q : Comment personnaliser l'apparence d'un module Odoo en utilisant Bootstrap sans modifier directement les fichiers CSS d'Odoo ?

Q : Quels sont les avantages et les limites de l'utilisation de Bootstrap dans le développement d'interfaces utilisateur pour Odoo ?

# Odoo et le Javascript

### Questions générales

Q : Peux-tu expliquer la différence entre le framework JavaScript legacy (Widgets) et OWL dans Odoo ?

Q : Quels sont les avantages d’OWL par rapport au système de widgets hérité d’Odoo ?

Q : Dans quel cas choisirais-tu encore d’utiliser le framework legacy au lieu d’OWL ?

### Questions sur les Widgets

Q : Comment fonctionne l’héritage dans le système de Widgets d’Odoo ?

Q : Qu’est-ce qu’un "QWeb template" et comment l’utiliser dans un widget ?

Q : Comment peux-tu communiquer entre deux widgets en JavaScript dans Odoo ?

Q : Comment attaches-tu un événement (click, change...) dans un widget et comment l’exécutes-tu ?

### Questions sur OWL

Q : Peux-tu expliquer comment est structuré un composant OWL et comment on le définit ? 

Q : Peux-tu expliquer comment fonctionne la gestion d’état (state) dans OWL ?

Q : Quelle est la différence entre les hooks onWillStart, onMounted et onWillUnmount dans OWL ?

Q : Comment faire passer des données d’un composant parent à un composant enfant en OWL ?

### Questions sur les requêtes RPC et la gestion asynchrone

Q : Comment fonctionnent les Promises en JavaScript dans Odoo, et pourquoi sont-elles utilisées dans les requêtes RPC ?

Q : Comment fais-tu une requête RPC en JavaScript dans Odoo pour récupérer des données d’un modèle ?

Q : Pourquoi utilise-t-on async/await pour les requêtes RPC au lieu des promesses classiques ?

Q : Que se passe-t-il si une requête RPC prend trop de temps à répondre ? Comment l’optimiser ?

Q : Comment créer une route JSON en Python dans Odoo et l’appeler en JavaScript ?


