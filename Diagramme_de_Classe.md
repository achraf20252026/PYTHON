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
