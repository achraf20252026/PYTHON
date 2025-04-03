# Diagramme de Classe

Ce document présente le diagramme de classe décrivant les principales entités du système et leurs relations.

## Entités Principales

- **Société** : Représente une entreprise proposant des espaces.
- **Utilisateur** : Représente toute personne utilisant la plateforme (clients ou administrateurs).
- **Administrateur** : Hérite de l'utilisateur et gère les espaces.
- **Espace** : Détail d’un espace (salle, bureau, etc.) proposé par une société.
- **Réservation** : Enregistrement d’une réservation d’un espace.
- **Paiement** : Détail d’un paiement (unique ou abonnement).
- **Abonnement** : Offre d’accès récurrent à des espaces.
- **Facture** et **Reçu** : Documents générés à la suite d’une transaction.

## Diagramme (PlantUML)

- [**Lien de l'image**](https://uml.planttext.com/plantuml/png/bLHBRjmm3DqRy1s4sRHDC46pDRf8aCykG96a1r1aZg52eWnA6g1e2_GQFK4pv_1DUfBAzjWZAPuYsSaapVT8FlB2EaxEQrKMGd5hsOCHijkvRiU-bmLZQoRhYabqumSQNR47HnARqS1h0ciXDfuoGG1qPNJhuFs7qSI_6k-0BcijKLf7t86dtlcpB2ReBqugQGVFwy11SwbIQFltrs-9Lf2a6Tl2bK444V0pn9JECgZS0lSfI0C4T6DRBi1c6KVhOYRthOMKlpA23nLBWwcdXhw4DdUSifPCQ-o4de7VTxlWsWxv5YdKeSvhUFAkOjVX-IWr71ot4dDp48VhWsC6OTu1OspbC5b4hrvqzZENe07T8Wrjq74CUJVAy8ZQz5DEGviwKnXiDc6U7cZw9H_iKp_nemJUseUm8t9p1sWzg8Xra9RngTO8qFWjg9STkUM1C2rBeuUzqTBQOTvvyKEp7etZANO3sEjmdpUN0dH__9knQd1XesokzW7d7eIVGTwnIsl3fHYaPilYS3LMvoksNhFLnxEparM-O1LhkcU2u_7xzQacdPT5V1G-_GYHQSeqO9_ba2_PY6gMJLaaZed3UKH061H0-9_GMU8Le-wvKI5qDlNmXyB2An9aA0wycm7eEC8unBvfEnpx5gM9uYPfnP5bSG5OXyF-3m00)

```
┌─────────────────────────┐     ┌───────────────┐                                  
│Société                  │     │Utilisateur    │                                  
├─────────────────────────┤     ├───────────────┤                                  
│- id: int                │     │- id: int      │                                  
│- nom: String            │     │- nom: String  │                                  
│- adresse: String        │     │- email: String│                                  
│+ creerCompte()          │     │+ s’inscrire() │                                  
│+ ajouterAdministrateur()│     │+ seConnecter()│                                  
└─────────────────────────┘     └───────────────┘                                  
                                                                                   
                                                                                   
                                ┌─────────────────────┐                            
            ┌────────────────┐  │Réservation          │                            
            │Administrateur  │  ├─────────────────────┤                            
            ├────────────────┤  │- id: int            │                            
            │- id: int       │  │- dateDebut: DateTime│                            
            │- niveau: String│  │- dateFin: DateTime  │                            
            │+ gererEspaces()│  │- statut: String     │                            
            └────────────────┘  │+ reserver()         │                            
                                │+ annuler()          │                            
                                └─────────────────────┘                            
                                                                                   
┌──────────────────────┐     ┌────────────────────────┐                            
│Espace                │     │Paiement                │  ┌────────────────────────┐
├──────────────────────┤     ├────────────────────────┤  │Reçu                    │
│- id: int             │     │- id: int               │  ├────────────────────────┤
│- type: String        │     │- montant: float        │  │- id: int               │
│- localisation: String│     │- datePaiement: DateTime│  │- dateEmission: DateTime│
│- description: String │     │- mode: String          │  │- details: String       │
│+ proposerEspace()    │     │+ effectuerPaiement()   │  │+ genererRecu()         │
└──────────────────────┘     └────────────────────────┘  └────────────────────────┘
                                          |                                        
                                                                                   
                              ┌─────────────────────┐                              
                              │Abonnement           │                              
                              ├─────────────────────┤                              
                              │- id: int            │                              
                              │- dateDebut: DateTime│                              
                              │- dateFin: DateTime  │                              
                              │- tarifMensuel: float│                              
                              │+ souscrire()        │                              
                              │+ renouveller()      │                              
                              └─────────────────────┘                              
                                          |                                        
                             ┌────────────────────────┐                            
                             │Facture                 │                            
                             ├────────────────────────┤                            
                             │- id: int               │                            
                             │- dateEmission: DateTime│                            
                             │- montantTotal: float   │                            
                             │+ genererFacture()      │                            
                             └────────────────────────┘


```





```plantuml
@startuml
class Société {
  - id: int
  - nom: String
  - adresse: String
  + creerCompte()
  + ajouterAdministrateur()
}

class Utilisateur {
  - id: int
  - nom: String
  - email: String
  + s’inscrire()
  + seConnecter()
}

class Administrateur {
  - id: int
  - niveau: String
  + gererEspaces()
}

class Espace {
  - id: int
  - type: String
  - localisation: String
  - description: String
  + proposerEspace()
}

class Réservation {
  - id: int
  - dateDebut: DateTime
  - dateFin: DateTime
  - statut: String
  + reserver()
  + annuler()
}

class Paiement {
  - id: int
  - montant: float
  - datePaiement: DateTime
  - mode: String
  + effectuerPaiement()
}

class Abonnement {
  - id: int
  - dateDebut: DateTime
  - dateFin: DateTime
  - tarifMensuel: float
  + souscrire()
  + renouveller()
}

class Facture {
  - id: int
  - dateEmission: DateTime
  - montantTotal: float
  + genererFacture()
}

class Reçu {
  - id: int
  - dateEmission: DateTime
  - details: String
  + genererRecu()
}

' Associations
Société "1" -- "0..*" Administrateur : gère
Société "1" -- "0..*" Espace : propose
Utilisateur <|-- Administrateur
Utilisateur "0..*" -- "0..*" Réservation : effectue
Réservation "1" -- "1" Espace : concerne
Réservation "1" -- "1" Paiement : règle
Paiement "0..1" -- "0..1" Abonnement : peut concerner
Réservation "1" -- "1" Reçu : génère
Abonnement "1" -- "1" Facture : génère

@enduml
