# Moteur de recherche et de recommandation de séries

Application web qui permet de chercher des séries TV par mot-clé et de recevoir des recommandations personnalisées. Projet réalisé en BUT3 Informatique (2023-2024).

Le prétraitement des sous-titres et le calcul de la matrice TF-IDF sont faits en Python dans le dépôt [Traitement-automatique-du-langage-naturel](https://github.com/Baran-Kaya-PS/Traitement-automatique-du-langage-naturel). Cette application charge le résultat et s'occupe de la recherche, des recommandations et de l'interface.

## Fonctionnalités

- **Recherche par mot-clé** : les séries sont classées selon le poids TF-IDF du mot dans leurs sous-titres.
- **Séries similaires** : similarité cosinus entre les vecteurs TF-IDF des séries, calculée au démarrage et mise en cache.
- **Recommandations** : filtrage collaboratif simple, à partir des séries aimées par les autres utilisateurs, en excluant celles que l'utilisateur a déjà aimées ou rejetées.
- **Comptes utilisateurs** : inscription, connexion (Spring Security), historique des « j'aime / je n'aime pas », suppression du compte.

## Stack

Java 17 · Spring Boot 3.2 (Web, Security, Data MongoDB) · Thymeleaf · MongoDB · Maven

## Lancer le projet

Prérequis : Java 17 et un MongoDB local sur le port 27017.

```bash
./mvnw spring-boot:run
```

L'application est accessible sur http://localhost:8081. Au premier lancement, les runners de `runners/` importent les données de `src/main/resources/data/` dans la base `SAE`, génèrent des utilisateurs de test et calculent les similarités.

## Organisation du code

```
controller/   routes web (recherche, séries, historique, comptes)
service/      recherche, recommandations, similarités
model/        Series, User, History, Evaluation, SeriesSimilarity
repository/   accès MongoDB
runners/      import des données et calculs au démarrage
utils/        calcul TF-IDF
```
