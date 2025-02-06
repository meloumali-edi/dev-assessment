# dev-assessment (15 - 20 min)

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
