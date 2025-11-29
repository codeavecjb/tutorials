# Formation complète en Data Engineering pour débutants

## Introduction
Aujourd'hui, explorons ensemble le monde du Data Engineering. Si vous souhaitez devenir Data Engineer et maîtriser les pipelines de données, vous êtes au bon endroit !

Abonnez-vous à ma chaîne YouTube **CodeAvecJB** pour ne rien manquer : https://www.youtube.com/@CodeAvecJB?sub_confirmation=1. On a plein de choses à explorer ensemble. 😊

### Sommaire
1. [Présentation du rôle de Data Engineer](#1-data-engineer--un-rôle-essentiel)
2. [Docker](#2-docker)
3. [SQL : les bases](#3-sql--les-bases-essentielles)
4. [Créer un pipeline de données](#4-créer-un-pipeline-de-données-à-partir-de-zéro)
5. [dbt (data build tool)](#5-dbt-data-build-tool)
6. [CRON Job / Airflow](#6-cron-job--airflow)

---
📩 Besoin d'aide pour coder ?
📺 YouTube : https://www.youtube.com/@CodeAvecJB/
📧 Contact : jb@codeavecjb.com
🌐 Site web : https://www.codeavecjb.com/

---

## 1. Data Engineer : Un rôle essentiel

### L'ingénierie des données : pilier de l'intelligence décisionnelle
L'ingénierie des données est le fondement sur lequel repose l'exploitation efficace de l'IA et du Big Data. Les entreprises qui aspirent à une prise de décision éclairée doivent investir dans une infrastructure de données robuste.

### Le rôle central du Data Engineer
Les data engineers sont les architectes et bâtisseurs de cet écosystème. Ils transforment des données brutes en informations structurées, fiables et exploitables. Sans cette transformation, les données restent un simple bruit.

### Un marché en pleine expansion
La demande explose pour des data engineers capables de :
- Concevoir des pipelines robustes et évolutifs.
- Gérer et optimiser le stockage (data lakes, data warehouses).
- Assurer la qualité, la sécurité et la gouvernance.
- Offrir un accès fiable aux équipes data.

### Les clés du succès
- **Prise de décision basée sur les données** : des infrastructures de qualité alimentent l'IA et le ML.
- **Gestion optimisée** : stockage, accès et traitement des données plus efficaces.
- **Qualité et sécurité** : processus rigoureux pour renforcer la confiance.
- **Innovation** : exploitation efficace des données = avantage concurrentiel.

### Rémunération et perspectives
Le salaire varie selon :
- La localisation (ex. : la Suisse offre des salaires élevés).
- L'expérience.
- Les compétences (Spark, Kafka, plateformes cloud...).
- La taille et le secteur de l'entreprise.
- Le niveau d'éducation.

---
📩 Besoin d'aide pour coder ?
📺 YouTube : https://www.youtube.com/@CodeAvecJB/
📧 Contact : jb@codeavecjb.com
🌐 Site web : https://www.codeavecjb.com/

---

## 2. Docker

- [ ] Rédiger un Dockerfile pour construire un conteneur.
- [ ] Créer une image Docker à partir du Dockerfile.
- [ ] Lancer l'application dans un conteneur Docker.
- [ ] Consulter la documentation Docker pour plus d'informations.
- [ ] Utiliser Docker Compose pour gérer plusieurs conteneurs.

Docker est une plateforme qui simplifie la création et l'exécution d'applications grâce aux conteneurs. Chaque conteneur embarque tout ce dont l'application a besoin : code, librairies et environnement.

> « Ça marche sur ma machine ! » devient réalité : la cohérence est garantie entre développement, test et production.

### Concepts fondamentaux
1. **Dockerfile** : une recette décrivant comment construire l'image.
2. **Image Docker** : la version instantanée de votre application.
3. **Conteneur Docker** : l'application en cours d'exécution.

### Comment ça fonctionne ?
- Dockerfile : rédigez les instructions.
- Image : construisez à partir du Dockerfile.
- Conteneur : lancez votre application de manière isolée.

### Ressources utiles
- https://docs.docker.com/get-started/introduction/get-docker-desktop/
- https://docs.docker.com/get-started/workshop/02_our_app/
- https://docs.docker.com/get-started/workshop/03_updating_app/
- https://docs.docker.com/get-started/workshop/05_persisting_data/
- https://docs.docker.com/get-started/workshop/07_multi_container/
- https://docs.docker.com/get-started/workshop/08_using_compose/

---
📩 Besoin d'aide pour coder ?
📺 YouTube : https://www.youtube.com/@CodeAvecJB/
📧 Contact : jb@codeavecjb.com
🌐 Site web : https://www.codeavecjb.com/

---

## 3. SQL : les bases essentielles

💡 Vous débutez avec SQL ? Regardez la vidéo dédiée : https://youtu.be/gRAKcefIXTE

SQL est le langage standard pour gérer et manipuler des bases relationnelles (CRUD : create, read, update, delete).

### Préparation
1. Créez un dossier `data-engineering-db`.
2. Téléchargez l'image officielle PostgreSQL :

```powershell
docker pull postgres
```

3. Démarrez un conteneur :

```powershell
docker run --name data-engineering-postgres -e POSTGRES_PASSWORD=secret -d postgres
```

4. Créez une base dans le conteneur :

```powershell
docker exec -u postgres data-engineering-postgres createdb postgresdb
```

5. Connectez-vous :

```powershell
docker exec -it data-engineering-postgres psql -U postgres -d postgresdb
```

Dans `psql`, utilisez `\dt` pour lister les tables.

### Requêtes de base

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

```sql
INSERT INTO users (username, email, password) VALUES
('alice123', 'alice@example.com', 'motdepasse123'),
('bob_smith', 'bob@example.org', 'securepass456'),
('charlie.d', 'charlie@example.net', 'p@$$wOrd789'),
('david.lee', 'david@example.io', 'mypassword'),
('eve.jones', 'eve@example.co', 'anotherpass');
```

```sql
SELECT * FROM users;
SELECT DISTINCT email FROM users;
UPDATE users
SET email = 'newbob@example.org'
WHERE email = 'bob@example.org';
```

### Exemple supplémentaire

```sql
CREATE TABLE films (
    id SERIAL PRIMARY KEY,
    titre VARCHAR(255) NOT NULL,
    realisateur VARCHAR(255),
    annee_sortie INT,
    genre VARCHAR(50)
);
```

```sql
INSERT INTO films (titre, realisateur, annee_sortie, genre) VALUES
('Inception', 'Christopher Nolan', 2010, 'Science-fiction'),
('Le Parrain', 'Francis Ford Coppola', 1972, 'Drame'),
('Parasite', 'Bong Joon-ho', 2019, 'Thriller'),
('Interstellar', 'Christopher Nolan', 2014, 'Science-fiction'),
('12 Hommes en colere', 'Sidney Lumet', 1957, 'Drame');
```

```sql
SELECT * FROM films WHERE genre = 'Science-fiction';
SELECT * FROM films WHERE annee_sortie > 2010;
UPDATE films SET annee_sortie = 2020 WHERE titre = 'Parasite';
```

---
📩 Besoin d'aide pour coder ?
📺 YouTube : https://www.youtube.com/@CodeAvecJB/
📧 Contact : jb@codeavecjb.com
🌐 Site web : https://www.codeavecjb.com/

---

## 4. Créer un pipeline de données à partir de zéro

```
Pipeline/
├── etl/
│   ├── Dockerfile
│   └── script.py
├── source_db_init/
│   └── init.sql
└── docker-compose.yaml
```

Créez `script.py` et `docker-compose.yaml`.

### Services Docker Compose

```yaml
services:
  source_postgres:
    image: postgres:15
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: source_db
    ports:
      - "5432:5432"
    networks:
      - etl_network
    volumes:
      - ./source_db_init/init.sql:/docker-entrypoint-initdb.d/init.sql

  destination_postgres:
    image: postgres:15
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: destination_db
    ports:
      - "5433:5432"
    networks:
      - etl_network

  etl_script:
    build:
      context: ./etl
      dockerfile: Dockerfile
    command: ["python", "script.py"]
    networks:
      - etl_network
    depends_on:
      - source_postgres
      - destination_postgres

networks:
  etl_network:
    driver: bridge
```

### Dockerfile `etl/Dockerfile`

```dockerfile
FROM python:3.8-slim

RUN apt-get update && apt-get install -y postgresql-client-15

COPY script.py .

CMD ["python", "script.py"]
```

### Script Python `script.py`

```python
import subprocess
import time
