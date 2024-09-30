---
title: Note de Conception - API de Gestion des Aéronefs

---

# Note de Conception - API de Gestion des Aéronefs

 Sabor Adam  
 BTS SIO  
 Lundi 30 septembre



## Modèle Conceptuel des Données

L’API gère trois entités principales :

1. **Aéronef** : Représente les avions à la base aérienne.
   - Propriétés : `id`, `nom`, `type`, `numero_serie`
2. **Technicien** : Représente les techniciens en charge des maintenances.
   - Propriétés : `id`, `nom`, `prenom`, `poste`
3. **Maintenance** : Enregistre les opérations de maintenance effectuées sur les aéronefs.
   - Propriétés : `id`, `date`, `type_maintenance`, `aeronef_id` (clé étrangère), `technicien_id` (clé étrangère)

### Relations entre les entités :
- Un **aéronef** peut avoir plusieurs **maintenances**.
- Un **technicien** peut effectuer plusieurs **maintenances**.
- La table **maintenance** est une table relationnelle qui relie les techniciens aux aéronefs sur lesquels ils effectuent des opérations.

## Modèle Physique de la Base de Données
![Capture d’écran 2024-09-30 à 10.54.34](https://hackmd.io/_uploads/Sy3Yu1dAA.png)
## 2. Liste des Endpoints

Voici les endpoints CRUD (Create, Read, Update, Delete) pour chaque entité dans l'API.

### Endpoints pour Avion

| Méthode  | Endpoint        | Description                                           |
| -------- | --------------- | ----------------------------------------------------- |
| `GET`    | `/aeronefs`      | Récupérer tous les avions.                            |
| `GET`    | `/aeronefs/:id`  | Récupérer un avion spécifique par son ID.             |
| `POST`   | `/aeronefs`      | Ajouter un nouvel avion.                              |
| `PUT`    | `/aeronefs/:id`  | Mettre à jour les informations d'un avion par son ID. |
| `DELETE` | `/aeronefs/:id`  | Supprimer un avion par son ID.                        |

### Endpoints pour Technicien

| Méthode  | Endpoint           | Description                                              |
| -------- | ------------------ | -------------------------------------------------------- |
| `GET`    | `/techniciens`      | Récupérer tous les techniciens.                          |
| `GET`    | `/techniciens/:id`  | Récupérer un technicien spécifique par son ID.           |
| `POST`   | `/techniciens`      | Ajouter un nouveau technicien.                           |
| `PUT`    | `/techniciens/:id`  | Mettre à jour les informations d'un technicien par son ID. |
| `DELETE` | `/techniciens/:id`  | Supprimer un technicien par son ID.                      |

### Endpoints pour Maintenance

| Méthode  | Endpoint            | Description                                                   |
| -------- | ------------------- | ------------------------------------------------------------- |
| `GET`    | `/maintenances`      | Récupérer toutes les maintenances effectuées.                 |
| `GET`    | `/maintenances/:id`  | Récupérer une maintenance spécifique par son ID.              |
| `POST`   | `/maintenances`      | Ajouter une nouvelle maintenance (lier un avion et un technicien). |
| `PUT`    | `/maintenances/:id`  | Mettre à jour les informations d'une maintenance par son ID.  |
| `DELETE` | `/maintenances/:id`  | Supprimer une maintenance par son ID.                         |
## 3. Liste des Erreurs Possibles

### Erreurs pour Avion

| Code d'erreur     | Description                                                | Exemple                                                                 |
|-------------------|------------------------------------------------------------|-------------------------------------------------------------------------|
| `404 Not Found`   | Avion avec l'ID spécifié n'existe pas                      | `/aeronefs/999` - avion avec l'ID 999 n'existe pas                      |
| `400 Bad Request` | Données incorrectes ou incomplètes dans la requête POST/PUT | POST `/aeronefs` sans numéro de série                                   |

### Erreurs pour Technicien

| Code d'erreur     | Description                                                | Exemple                                                                 |
|-------------------|------------------------------------------------------------|-------------------------------------------------------------------------|
| `404 Not Found`   | Technicien avec l'ID spécifié n'existe pas                 | `/techniciens/999` - technicien avec l'ID 999 n'existe pas              |
| `400 Bad Request` | Données incorrectes ou incomplètes dans la requête POST/PUT | POST `/techniciens` avec un champ obligatoire manquant                  |

### Erreurs pour Maintenance

| Code d'erreur     | Description                                                | Exemple                                                                 |
|-------------------|------------------------------------------------------------|-------------------------------------------------------------------------|
| `404 Not Found`   | Maintenance avec l'ID spécifié n'existe pas                | `/maintenances/999` - maintenance avec l'ID 999 n'existe pas            |
| `400 Bad Request` | Données incorrectes ou incomplètes dans la requête POST/PUT | POST `/maintenances` sans spécifier `aeronef_id` ou `technicien_id`     |
## 4. Présentation du Schéma Conceptuel

Le schéma ci-dessous représente le **modèle conceptuel des données** pour l'API de gestion des aéronefs, techniciens et maintenances. Ce modèle repose sur trois entités principales : **Avion**, **Technicien** et **Maintenance**, qui sont liées entre elles par des relations spécifiques.
### Schéma Conceptuel
![Capture d’écran 2024-09-30 à 11.28.06](https://hackmd.io/_uploads/S1hVWxuR0.png)

Vous pouvez retrouver l'intégralité du code source et l'évolution du projet sur le dépôt GitHub suivant :

[Mon dépôt GitHub](https://github.com/adamsabor/Api-Avion-)


