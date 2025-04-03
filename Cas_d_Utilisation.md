# Cas d'Utilisation

Ce document décrit les principaux cas d’utilisation de la plateforme ainsi que les acteurs impliqués.

## Acteurs

- **Super Administrateur** : Crée le compte société et gère les administrateurs.
- **Administrateur** : Gère les espaces (ajout, modification, suppression) et supervise les réservations.
- **Utilisateur/Client** : Parcourt les espaces proposés, effectue des réservations et réalise les paiements (paiement unique ou abonnement).
- **Système de Paiement** : Externe ou intégré pour la validation des transactions.
- **Module de Facturation** : Génère automatiquement les reçus et factures.

## Cas d’Utilisation Principaux

- **Super Administrateur**
  - Créer le compte de société.
  - Ajouter des administrateurs.

- **Administrateur**
  - Gérer les espaces (ajout, modification, suppression).
  - Valider les réservations.

- **Utilisateur/Client**
  - Parcourir les espaces disponibles.
  - Réserver un espace.
  - Effectuer le paiement (paiement unique ou abonnement).

- **Système de Paiement**
  - Valider la transaction lors du paiement.

- **Module de Facturation**
  - Générer le reçu et la facture après la réservation.

## Diagramme de Cas d'Utilisation (PlantUML)

```plantuml
@startuml
actor "Super Administrateur" as SA
actor "Administrateur" as A
actor "Utilisateur/Client" as U
actor "Système de Paiement" as SP
actor "Module de Facturation" as MF

rectangle "Plateforme de Coworking" {
  SA --> (Créer Compte Société)
  SA --> (Ajouter Administrateur)
  
  A --> (Gérer Espaces)
  A --> (Valider Réservations)
  
  U --> (Parcourir Espaces)
  U --> (Réserver Espace)
  U --> (Effectuer Paiement)
  
  (Réserver Espace) --> (Générer Reçu)
  (Réserver Espace) --> (Générer Facture)
  
  (Effectuer Paiement) --> SP : "Valider Transaction"
  (Générer Facture) --> MF : "Émettre Facture"
}
@enduml
