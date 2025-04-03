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

-  [**Lien de image**](https://uml.planttext.com/plantuml/png/ZP9DJiCm48NtaNA7KLPqKR5dWLf5BQjAKKFPMycqCYHsDHw34E80d0Ho3b-CgTEaHUs2XJT-ttlpOyySAsBVDccYAhO4MUdtI32lMssqOrACdZ9G3ihvo5nHJ-A6TQDTL6xpHgFX26nE5TuTXvyMeKOebCPsGCfYP5QszaqabdBZfP2s9aAhPPga2M75okm4oOf6QcqjzO6vVRFqeiqkWuyq0UaQfjDxkCafT39NRjiz8vIsqg7Zq4tEcVcpzNmnV4GEvqWzX8u4MhYzgj1DpfGdrUXQf7Ne7D9hxDcDzaqF5Oegwqd_JJYAH-SOVwujjbiPseisB6sCllIDhPg-spM6Rp_v7zjl74_fLof7Jrd07MJ3r8-aZ1FhuQ6YxJ8nkbRBWojyjSXCm_kYM3xJP8Qcbi_u2m00)

```

             ┌────────────────────┐                          ┌──────────────┐                                     ┌──────────────────┐                       
             │Super Administrateur│                          │Administrateur│                                     │Utilisateur/Client│                       
             ├────────────────────┤                          ├──────────────┤                                     ├──────────────────┤                       
             └────────────────────┘                          └──────────────┘                                     └──────────────────┘                       
                                                                                                                            |                                
                                                                                                                            |                                
┌────────────────────┐  ┌──────────────────────┐   ┌─────────────┐   ┌────────────────────┐   ┌─────────────────┐   ┌───────────────┐   ┌──────────────────┐ 
│Créer Compte Société│  │Ajouter Administrateur│   │Gérer Espaces│   │Valider Réservations│   │Parcourir Espaces│   │Réserver Espace│   │Effectuer Paiement│ 
├────────────────────┤  ├──────────────────────┤   ├─────────────┤   ├────────────────────┤   ├─────────────────┤   ├───────────────┤   ├──────────────────┤ 
└────────────────────┘  └──────────────────────┘   └─────────────┘   └────────────────────┘   └─────────────────┘   └───────────────┘   └──────────────────┘ 
                                                                                                                            |                                
                                                                                                   ┌────────────┐   ┌───────────────┐   ┌───────────────────┐
                                                                                                   │Générer Reçu│   │Générer Facture│   │Système de Paiement│
                                                                                                   ├────────────┤   ├───────────────┤   ├───────────────────┤
                                                                                                   └────────────┘   └───────────────┘   └───────────────────┘
                                                                                                                            |                                
                                                                                                                                                             
                                                                                                                 ┌─────────────────────┐                     
                                                                                                                 │Module de Facturation│                     
                                                                                                                 ├─────────────────────┤                     
                                                                                                                 └─────────────────────┘                     

```

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
