# Spring Boot + MySQL conteneurisés avec Docker Compose

TP réalisé dans le cadre du cycle ingénieur ISIC (ENSA El Jadida) : conteneuriser une application Spring Boot et sa base MySQL, puis les orchestrer avec Docker Compose.

## Objectif
Déployer une application Java avec sa base de données en une seule commande, de façon reproductible sur n'importe quelle machine.

## Ce que j'ai fait
- Écriture du `Dockerfile` de l'application (image `eclipse-temurin:17`, jar Spring Boot exposé sur le port 8080).
- Écriture du `docker-compose.yml` : un service `mysql-db` (MySQL 8.0 avec volume persistant `mysql-data`) et un service `spring-app`.
- Configuration de la connexion à la base par variables d'environnement (`SPRING_DATASOURCE_*`).
- Gestion du démarrage : `depends_on` et `restart: on-failure` pour relancer l'application si MySQL n'est pas encore prêt.

## Technologies
Java 17 · Spring Boot · Spring Data JPA · MySQL 8 · Docker · Docker Compose · Maven

## Lancer le projet
```bash
./mvnw clean package -DskipTests
docker build -t ens/springdocker:1.0 .
docker compose up -d
```
L'application est ensuite disponible sur http://localhost:8080 et MySQL sur le port 3307.

## Ce que j'ai appris
Construire une image applicative, faire communiquer des conteneurs par leur nom de service, persister des données avec un volume et gérer l'ordre de démarrage des services.
