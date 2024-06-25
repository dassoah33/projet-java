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

## Explication des Fichiers du Projet

- **Main.java** : Point d'entrée de l'application Spring Boot. Il initialise et lance l'application.
- **ImmatController.java** : Ce contrôleur gère les requêtes HTTP pour consulter les informations des aéronefs par leur immatriculation et pour recharger le fichier CSV contenant les données des aéronefs.
- **PlanespottersAPI.java** : Cette classe gère l'interaction avec l'API Planespotters pour obtenir des informations supplémentaires sur les aéronefs en utilisant leur immatriculation.
- **ImmatService.java** : Ce service contient la logique métier pour lire les données des aéronefs à partir du fichier CSV et pour obtenir des informations supplémentaires à partir de l'API Planespotters.
- **ImmatCSVReader.java** : Cette classe lit et parse le fichier CSV contenant les informations des aéronefs et les stocke dans une structure de données interne pour une utilisation ultérieure.
- **Config.java** : Cette classe de configuration déclare les beans nécessaires à l'application, ici le bean pour ImmatCSVReader.
- **AppConf.java** : Cette classe de configuration lit les propriétés du fichier application.properties, notamment le nom du fichier CSV à utiliser.
- **AeronefDTO.java** : Classe DTO pour transporter les informations des aéronefs.

## Améliorations

1. **Ajout d'un Message de Log pour `getAeronefFromImmat`** :
    - Un message de log a été ajouté dans la méthode `getAeronefFromImmat` de la classe `ImmatService` pour signaler son utilisation.
    - Code ajouté :
    ```java
    logger.info("Utilisation de getAeronefFromImmat() avec immatriculation: " + immat);
    ```

2. **Traitement Insensible à la Casse des Immatriculations** :
    - La méthode `getAeronefFromImmat` a été modifiée pour accepter les immatriculations aussi bien en majuscule qu’en minuscule. Cela a été fait en convertissant les immatriculations en majuscule avant de les traiter.
    - Code ajouté :
    ```java
    var entry = immatCSVReader.getEntryByImmat(immat.toUpperCase());
    ```

3. **Ajout d'une Nouvelle Variable de Configuration `immataeronef.dateExtract`** :
    - Une nouvelle variable de configuration `immataeronef.dateExtract` a été ajoutée dans la classe `AppConf`.
    - Cette variable est lue à partir du fichier `application.properties`.
    - Code ajouté dans `AppConf.java` :
    ```java
    @ConfigurationProperties("immataeronef")
    public class AppConf {
        private String filename;
        private String dateExtract; // nouvelle variable de configuration
    }
    ```

4. **Ajout de la Variable `dateExtract` au DTO de Retour** :
    - La classe `AeronefDTO` a été modifiée pour inclure un nouveau champ `dateExtract`.
    - Ce champ est utilisé pour ajouter la date d'extraction dans le retour du contrôleur.
    - Code ajouté dans `AeronefDTO.java` :
    ```java
    public class AeronefDTO {
        private String immatriculation;  
        private String constructeur;
        private String modele;
        private String aerodromeAttache;
        private String dateExtract; // nouveau champ
    }
    ```

    - Modification du contrôleur `ImmatController.java` :
    ```java
    @GetMapping("/aeronef/{immat}")
    public AeronefDTO getAeronef(@PathVariable("immat") String immat, HttpServletResponse response) {
        var result = immatService.getAeronefFromImmat(immat);
        if (result.isEmpty()) {
            response.setStatus(SC_NO_CONTENT);
            return null;
        }
        var aeronef = result.get();
        aeronef.setDateExtract(appConf.getDateExtract()); // ajouter la date d'extraction
        return aeronef;
    }
    ```

## Auteurs

- Najath Hikmath LAWANI
- Nidele MANKEU
- Dassoah Maixent OKOUMOU

## License