
# Projet Neo4j-OFMS

Ce projet utilise Neo4j pour créer une base de données graphique qui modélise des transactions entre clients et distributeurs. Actuellement, le modèle se base sur les transactions effectuées par les clients et les distributeurs.

## Table des matières

1. [Configuration](#configuration)
2. [Prérequis](#prérequis)
3. [Installation](#installation)
4. [Démarrer avec Neo4j](#démarrer-avec-neo4j)
5. [Utilisation](#utilisation)
6. [Analyse de données avec Neo4j](#analyse-de-données-avec-neo4j)
7. [Gestion des erreurs](#gestion-des-erreurs)
8. [Zoom sur le cercle client](#zoom-sur-le-cercle-client)

## Configuration

Ce projet est construit avec Neo4j et utilise le langage Cypher pour manipuler les données. Avant de continuer, assurez-vous que Neo4j est correctement installé et configuré sur votre système.

### Prérequis

- Neo4j Desktop
- Java 11 ou supérieur (requis pour Neo4j)

### Installation

Vous pouvez installer la dernière version de Neo4j Desktop sur votre ordinateur, ou utiliser Neo4j Aura pour une expérience directement dans votre navigateur.

- [Lien d'installation Neo4j Desktop](https://neo4j.com/download/)
- [Lien Neo4j Aura](https://login.neo4j.com/u/login/identifier?state=hKFo2SBRZHhlUFQ5dXVyaWd4NkFwcVJYWnUtUm9TODZvYXNhbaFur3VuaXZlcnNhbC1sb2dpbqN0aWTZIHBuMFV1eFFhZjlhZ2docUE2R3puYkZOTXMzbTBlNXBSo2NpZNkgV1NMczYwNDdrT2pwVVNXODNnRFo0SnlZaElrNXpZVG8)

## Démarrer avec Neo4j

Une fois l’installation effectuée, suivez ces étapes pour créer votre premier projet Neo4j :

### Création du projet

1. **Créer un nouveau projet** : Cliquez sur "New", puis "Create Project".

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/99d5d21a-d851-4238-a9ea-5f69f79ceab7)

2. **Ajouter une base de données** : Cliquez sur "Add". Choisissez "Local DBMS" pour utiliser Neo4j localement ou "Remote connection" pour utiliser Aura DB.

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/41580665-db57-4571-9ee0-49ca15c3b41e)

3. **Activer la base de données** : Cliquez sur "start", puis utilisez le menu à côté du bouton "ouvrir" pour choisir entre Neo4j Browser, Neo4j Bloom, etc.

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/c765d3e0-d47a-4422-bebe-db1e19faf99b)

## Utilisation

Le projet modélise des transactions entre clients et distributeurs. Les relations "Transaction" incluent des propriétés comme "Service", "Volume", et "Value".

## Analyse de données avec Neo4j

### Centrality Algorithms

Les algorithmes de centralité mesurent l'importance des nœuds dans le réseau. Voici quelques algorithmes courants :

- **Betweenness Centrality** : Identifie les nœuds servant de ponts dans le réseau.
- **PageRank** : Évalue l'importance des nœuds en fonction des liens entrants.

### Weakly Connected Components

Cet algorithme identifie les parties du graphe non reliées aux autres, utile pour vérifier l'interconnexion des parties de votre réseau.

## Gestion des erreurs

![Erreur](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/051a06e3-6abd-4c72-8a89-d93b7b69647c)

1. Cliquez sur la base de données concernée.
2. Accédez à "Plugins" à droite, cliquez sur APOC, puis "Install" et "Restart".

![APOC](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/d088d6bf-7402-4958-83ab-d5eb2c569447)

En cas d’erreur liée à Graph Data Science, suivez les mêmes étapes. Pour les erreurs de configuration, modifiez le fichier `neo4j.conf` pour décommenter `dbms.security.allow_csv_import_from_file_urls=true`.

![Configuration](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/f3436f2e-4c03-4239-93db-a0b0fb4d1adf)

## Zoom sur le cercle client

### Clients extrêmement risqués dans la période du 01/01/2024

![Graphique](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/e0886775-dea8-4072-ae39-4a4052c8f6b5)
