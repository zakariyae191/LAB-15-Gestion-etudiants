# SQLiteStudentCRUD

## Objectif

L'objectif de ce TP est de créer une application Android simple qui permet de gérer des étudiants avec une base de données SQLite locale.

L'application montre comment créer un modèle métier, initialiser une base SQLite avec `SQLiteOpenHelper`, séparer la logique CRUD dans un service, tester les données avec Logcat, puis connecter cette logique à une interface XML.

## Fonctionnalités

- Ajouter un étudiant
- Chercher un étudiant par ID
- Supprimer un étudiant par ID
- Afficher les données dans Logcat
- Utiliser `SQLiteOpenHelper`
- Utiliser un service CRUD

## Technologies utilisées

- Java
- Android Studio
- SQLite
- SQLiteOpenHelper
- SQLiteDatabase
- ContentValues
- Cursor
- Toast
- Logcat

## Architecture du projet

- `projet.fst.ma.app.classes.Etudiant`
- `projet.fst.ma.app.util.MySQLiteHelper`
- `projet.fst.ma.app.service.EtudiantService`
- `projet.fst.ma.app.MainActivity`

## Description des étapes

### Étape 1 : Création du projet

Le projet a été créé dans Android Studio avec le langage Java, une activité vide et le package `projet.fst.ma.app`.

### Étape 2 : Création de la classe Etudiant

La classe `Etudiant` est la classe modèle. Elle contient les attributs `id`, `nom` et `prenom`.

L'attribut `id` représente la clé primaire générée automatiquement par SQLite. Les attributs `nom` et `prenom` représentent les informations de l'étudiant.

### Étape 3 : Création de MySQLiteHelper

La classe `MySQLiteHelper` hérite de `SQLiteOpenHelper`. Elle crée la base de données locale nommée `ecole` et la table `etudiant`.

La méthode `onCreate()` crée la table. La méthode `onUpgrade()` supprime puis recrée la table si la version de la base change.

### Étape 4 : Création de EtudiantService

La classe `EtudiantService` contient les méthodes CRUD :

- `create` : ajouter un étudiant
- `update` : modifier un étudiant
- `findById` : chercher un étudiant par ID
- `delete` : supprimer un étudiant
- `findAll` : afficher tous les étudiants

Cette classe permet de séparer la logique de base de données de l'interface graphique.

### Étape 5 : Test avec Logcat

Une première version de `MainActivity` peut être utilisée pour insérer, afficher et supprimer des étudiants en vérifiant les résultats dans Logcat.

Après ce test, il faut utiliser la version finale de `MainActivity` avec l'interface graphique afin d'éviter les insertions répétées à chaque lancement de l'application.

### Étape 6 : Création de l'interface

L'interface contient des champs pour saisir le nom, le prénom et l'ID de l'étudiant. Elle contient aussi les boutons `Valider`, `Chercher` et `Supprimer`.

Le `TextView` nommé `res` affiche le résultat de la recherche.

### Étape 7 : Connexion interface-service

Chaque bouton appelle une méthode de `EtudiantService`.

Le bouton `Valider` appelle `create()`. Le bouton `Chercher` appelle `findById()`. Le bouton `Supprimer` appelle `delete()`.

### Étape 8 : Test final

Pour tester l'application :

1. Saisir un nom et un prénom.
2. Cliquer sur `Valider`.
3. Saisir l'ID de l'étudiant.
4. Cliquer sur `Chercher`.
5. Cliquer sur `Supprimer` pour supprimer l'étudiant trouvé.
6. Chercher le même ID pour vérifier que l'étudiant n'existe plus.

## Résultat attendu

L'ajout d'un étudiant l'enregistre dans SQLite.

La recherche par ID affiche le nom et le prénom de l'étudiant.

La suppression par ID retire l'étudiant de la base de données.

Des messages Toast confirment chaque action, et la liste des étudiants est affichée dans Logcat après chaque ajout.

## Captures d'écran

![Interface principale](screenshots/interface.png)

![Ajout étudiant](screenshots/add.png)

![Recherche étudiant](screenshots/search.png)

![Suppression étudiant](screenshots/delete.png)

![Logcat](screenshots/logcat.png)

## Explication des concepts

### SQLiteOpenHelper

`SQLiteOpenHelper` est une classe utilisée pour créer et gérer une base SQLite locale.

La méthode `onCreate()` crée les tables de la base de données.

La méthode `onUpgrade()` gère les changements de version de la base.

### SQLiteDatabase

`SQLiteDatabase` permet d'exécuter des opérations sur la base de données.

`getWritableDatabase()` permet d'insérer, modifier ou supprimer des données.

`getReadableDatabase()` permet de lire les données.

### ContentValues

`ContentValues` est utilisé pour préparer les valeurs à insérer ou à modifier dans la base de données.

Exemple :

```java
values.put("nom", e.getNom());
```

### Cursor

`Cursor` représente le résultat d'une requête SQL.

`moveToFirst()` permet de lire la première ligne du résultat.

`getInt()` et `getString()` permettent de récupérer les valeurs des colonnes.

### Service

`EtudiantService` sépare la logique CRUD de l'interface.

`MainActivity` appelle le service sans écrire directement les requêtes SQLite.

### CRUD

- Create : ajouter un étudiant
- Read : chercher un étudiant ou afficher tous les étudiants
- Update : modifier un étudiant
- Delete : supprimer un étudiant

## Conclusion

Ce TP montre comment structurer une application Android avec une classe modèle, un helper SQLite, une couche service et une interface simple pour effectuer des opérations CRUD.
