# Diagramme de Séquence

Ce document décrit le déroulement d'une réservation d'espace par un utilisateur, depuis la consultation des espaces jusqu'à la confirmation de la réservation et la génération des documents de paiement.

## Scénario de Réservation

1. L'utilisateur se connecte et consulte les espaces disponibles.
2. L'utilisateur sélectionne un espace et initie une réservation.
3. Le système vérifie la disponibilité de l'espace.
4. L'utilisateur procède au paiement via le système de paiement.
5. Le système de paiement confirme la transaction.
6. Le système enregistre la réservation et génère le reçu.
7. En cas d’abonnement, le module de facturation génère également une facture.

## Diagramme (PlantUML)

- [Lien de l'image](https://uml.planttext.com/plantuml/png/VLD1Rjim4BmBq1yMlZG1KkJkGv72XGiV11XItPvfUTLi894gkGpGt_JMw1twM9UYPDDkKTqapipEp59FZfLbtxLvfces5bO7ffQSOlHs1Sh18SzwWL1DlT8Cgvrcj8sg4RxXyR4mHsen0dStoEgdu_6jGpWXbEFWqBug9gCdT5N-1xrNX1rgZiZz3R8m9zzEkAruzlOYMcppBCyEyFw3k5b3XL0RhR4Mnu0SNfnlmqkB3j3rai89VXS8LRc6JzWfBRfI0Ck0TsT8LIwQ9RBnLcCg0ITolT5qR0CsDJ0EhKodO0Aydl712cbY4X45DcaczRAH0t7gXNaDYLu2vEiuM6f8K8i1MHsFG-ftOtH3DjHw0rbc7TRmiMceVewHJ1-ckD1kFsy1xhoc7nuVrJ442P_kav2RPqEEMDWNXYHqQlxg96nZR3VPlzIzNyCNgxJhaDdY6NSrMOBi_meYdN4WgZhsaPPMHB7n5xp8bcxh1VMATUepBUhpEEZnRN825iVVFXYvRbx-aPQX8hWKaMSWJrGfjkSRPE5xa1lYtOHckgSOmSLsSHllqdAwK6JjgMhmjYpeh8FwzCyDrh6aQUh374DsSJSJxmFfISZJ3_y7)

```

          ┌─┐                                                                                                                                                                                         
          ║"│                                                                                                                                                                                         
          └┬┘                                                                                                                                                                                         
          ┌┼┐                                                                                                                                                                                         
           │                                         ┌────────────────────┐                        ┌──────────────────────┐           ┌───────────────────┐          ┌─────────────────────┐          
          ┌┴┐                                        │Interface Web/Mobile│                        │Système de Réservation│           │Système de Paiement│          │Module de Facturation│          
      Utilisateur                                    └──────────┬─────────┘                        └───────────┬──────────┘           └─────────┬─────────┘          └──────────┬──────────┘          
           │       Se connecter et consulter les espaces        │                                              │                                │                               │                     
           │───────────────────────────────────────────────────>│                                              │                                │                               │                     
           │                                                    │                                              │                                │                               │                     
           │                                                    │           Demande liste d'espaces            │                                │                               │                     
           │                                                    │─────────────────────────────────────────────>│                                │                               │                     
           │                                                    │                                              │                                │                               │                     
           │                                                    │      Retourne les espaces disponibles        │                                │                               │                     
           │                                                    │<─────────────────────────────────────────────│                                │                               │                     
           │                                                    │                                              │                                │                               │                     
           │  Sélectionne un espace et initie la réservation    │                                              │                                │                               │                     
           │───────────────────────────────────────────────────>│                                              │                                │                               │                     
           │                                                    │                                              │                                │                               │                     
           │                                                    │            Créer une réservation             │                                │                               │                     
           │                                                    │─────────────────────────────────────────────>│                                │                               │                     
           │                                                    │                                              │                                │                               │                     
           │                                                    │                                              │────┐                           │                               │                     
           │                                                    │                                              │    │ Vérifier disponibilité    │                               │                     
           │                                                    │                                              │<───┘                           │                               │                     
           │                                                    │                                              │                                │                               │                     
           │                                                    │           Confirme disponibilité             │                                │                               │                     
           │                                                    │<─────────────────────────────────────────────│                                │                               │                     
           │                                                    │                                              │                                │                               │                     
           │Affiche les options de paiement (unique/abonnement) │                                              │                                │                               │                     
           │<───────────────────────────────────────────────────│                                              │                                │                               │                     
           │                                                    │                                              │                                │                               │                     
           │  Choisit le paiement et saisit les informations    │                                              │                                │                               │                     
           │───────────────────────────────────────────────────>│                                              │                                │                               │                     
           │                                                    │                                              │                                │                               │                     
           │                                                    │                      Transmettre les infos de paiement                        │                               │                     
           │                                                    │──────────────────────────────────────────────────────────────────────────────>│                               │                     
           │                                                    │                                              │                                │                               │                     
           │                                                    │                           Confirme la transaction                             │                               │                     
           │                                                    │<──────────────────────────────────────────────────────────────────────────────│                               │                     
           │                                                    │                                              │                                │                               │                     
           │                                                    │Mettre à jour la réservation avec le paiement │                                │                               │                     
           │                                                    │─────────────────────────────────────────────>│                                │                               │                     
           │                                                    │                                              │                                │                               │                     
           │                                                    │        Génère le reçu de réservation         │                                │                               │                     
           │                                                    │<─────────────────────────────────────────────│                                │                               │                     
           │                                                    │                                              │                                │                               │                     
           │                                                    │                                              │                                │                               │                     
           │                               ╔══════╤═════════════╪══════════════════════════════════════════════╪════════════════════════════════╪═══════════════════════════════╪════════════════════╗
           │                               ║ ALT  │  Si abonnement                                             │                                │                               │                    ║
           │                               ╟──────┘             │                                              │                                │                               │                    ║
           │                               ║                    │                                              │                  Demander génération facture                   │                    ║
           │                               ║                    │                                              │───────────────────────────────────────────────────────────────>│                    ║
           │                               ║                    │                                              │                                │                               │                    ║
           │                               ║                    │                                              │                    Retour facture générée                      │                    ║
           │                               ║                    │                                              │<───────────────────────────────────────────────────────────────│                    ║
           │                               ║                    │                                              │                                │                               │                    ║
           │                               ║                    │               Affiche facture                │                                │                               │                    ║
           │                               ║                    │<─────────────────────────────────────────────│                                │                               │                    ║
           │                               ╚════════════════════╪══════════════════════════════════════════════╪════════════════════════════════╪═══════════════════════════════╪════════════════════╝
           │                                                    │                                              │                                │                               │                     
           │      Affiche confirmation, reçu et (facture)       │                                              │                                │                               │                     
           │<───────────────────────────────────────────────────│                                              │                                │                               │                     
      Utilisateur                                    ┌──────────┴─────────┐                        ┌───────────┴──────────┐           ┌─────────┴─────────┐          ┌──────────┴──────────┐          
          ┌─┐                                        │Interface Web/Mobile│                        │Système de Réservation│           │Système de Paiement│          │Module de Facturation│          
          ║"│                                        └────────────────────┘                        └──────────────────────┘           └───────────────────┘          └─────────────────────┘          
          └┬┘                                                                                                                                                                                         
          ┌┼┐                                                                                                                                                                                         
           │                                                                                                                                                                                          
          ┌┴┐                                                                                                                                                                                         


```

```plantuml
@startuml
actor "Utilisateur" as U
participant "Interface Web/Mobile" as UI
participant "Système de Réservation" as SR
participant "Système de Paiement" as SP
participant "Module de Facturation" as MF

U -> UI: Se connecter et consulter les espaces
UI -> SR: Demande liste d'espaces
SR -> UI: Retourne les espaces disponibles

U -> UI: Sélectionne un espace et initie la réservation
UI -> SR: Créer une réservation
SR -> SR: Vérifier disponibilité
SR -> UI: Confirme disponibilité

UI -> U: Affiche les options de paiement (unique/abonnement)
U -> UI: Choisit le paiement et saisit les informations
UI -> SP: Transmettre les infos de paiement
SP -> UI: Confirme la transaction

UI -> SR: Mettre à jour la réservation avec le paiement
SR -> UI: Génère le reçu de réservation

alt Si abonnement
    SR -> MF: Demander génération facture
    MF -> SR: Retour facture générée
    SR -> UI: Affiche facture
end

UI -> U: Affiche confirmation, reçu et (facture)

@enduml

