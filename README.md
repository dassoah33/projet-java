# Annuaire des Immatriculations des Aéronefs en France

## Description du Projet

Ce projet est une application Spring Boot conçue pour gérer un annuaire des immatriculations des aéronefs en France. Les informations sur les aéronefs sont stockées dans un fichier CSV et peuvent être consultées via des requêtes HTTP. En outre, le projet intègre l'API Planespotters pour obtenir des informations supplémentaires sur les aéronefs.

## Fonctionnalités Principales

1. **Consultation des informations des aéronefs** : Les utilisateurs peuvent consulter les informations des aéronefs en utilisant leur immatriculation.
2. **Rechargement du fichier CSV** : Le fichier CSV contenant les informations des aéronefs peut être rechargé sans redémarrer l'application.
3. **Intégration avec l'API Planespotters** : Permet d'obtenir des photos et des informations supplémentaires sur les aéronefs à partir de l'API Planespotters.

## Architecture du Projet

Le projet suit une architecture typique de Spring Boot avec les composants suivants :

- **Contrôleur** : Gère les requêtes HTTP et renvoie les réponses appropriées.
- **Service** : Contient la logique métier pour traiter les données des aéronefs.
- **Lecteur CSV** : Lit les données des aéronefs à partir d'un fichier CSV.
- **Intégration API** : Interagit avec l'API Planespotters pour obtenir des informations supplémentaires sur les aéronefs.

## Description de la Technologie Utilisée

- **Spring Boot** : Simplifie le développement d'applications en utilisant une configuration par défaut et des conventions tout en permettant des personnalisations. Il facilite la création d'applications Java basées sur le modèle MVC (Model-View-Controller).
- **API Planespotters** : Cette API est utilisée pour enrichir les données des aéronefs avec des photos et des informations supplémentaires, offrant ainsi une expérience utilisateur plus riche et plus complète.

## Prérequis

- Java 8 ou supérieur
- Maven
- Accès à Internet pour l'intégration de l'API Planespotters

## Installation et Démarrage

1. **Cloner le dépôt** :
    ```bash
    git clone https://github.com/votre-utilisateur/votre-depot.git
    cd votre-depot
    ```

2. **Construire le projet** :
    ```bash
    mvn clean install
    ```

3. **Configurer le fichier `application.properties`** :
    Dans le répertoire `src/main/resources`, modifiez le fichier `application.properties` pour inclure le nom du fichier CSV à utiliser et d'autres configurations nécessaires.

4. **Lancer l'application** :
    ```bash
    mvn spring-boot:run
    ```

## Utilisation

### Endpoints Disponibles

1. **Consultation d'un aéronef par immatriculation** :
    - **URL** : `/aeronef/{immat}`
    - **Méthode HTTP** : `GET`
    - **Description** : Retourne les informations de l'aéronef correspondant à l'immatriculation donnée.
    - **Exemple** : `GET http://localhost:8080/aeronef/F-ABCD`

2. **Rechargement du fichier CSV** :
    - **URL** : `/aeronef/reload`
    - **Méthode HTTP** : `POST`
    - **Description** : Recharge le fichier CSV contenant les informations des aéronefs sans redémarrer l'application.
    - **Exemple** : `POST http://localhost:8080/aeronef/reload`

### Fonctionnement

- L'application lit un fichier CSV contenant les informations des aéronefs et les stocke en mémoire.
- Lorsqu'une requête est effectuée pour obtenir les informations d'un aéronef, l'application recherche dans les données en mémoire et retourne les informations correspondantes.
- L'intégration avec l'API Planespotters permet d'enrichir les données retournées avec des photos et d'autres informations disponibles via cette API.

## Explication des Fichiers du Projet

- **Main.java** : Point d'entrée de l'application Spring Boot. Il initialise et lance l'application.
- **ImmatController.java** : Ce contrôleur gère les requêtes HTTP pour consulter les informations des aéronefs par leur immatriculation et pour recharger le fichier CSV contenant les données des aéronefs.
- **PlanespottersAPI.java** : Cette classe gère l'interaction avec l'API Planespotters pour obtenir des informations supplémentaires sur les aéronefs en utilisant leur immatriculation.
- **ImmatService.java** : Ce service contient la logique métier pour lire les données des aéronefs à partir du fichier CSV et pour obtenir des informations supplémentaires à partir de l'API Planespotters.
- **ImmatCSVReader.java** : Cette classe lit et parse le fichier CSV contenant les informations des aéronefs et les stocke dans une structure de données interne pour une utilisation ultérieure.
- **Config.java** : Cette classe de configuration déclare les beans nécessaires à l'application, ici le bean pour ImmatCSVReader.
- **AppConf.java** : Cette classe de configuration lit les propriétés du fichier application.properties, notamment le nom du fichier CSV à utiliser.
- **AeronefDTO.java** : Classe DTO pour transporter les informations des aéronefs.

## Auteurs

- Najath Hikmath LAWANI
- Nidele MANKEU
- Dassoah Maixent OKOUMOU
