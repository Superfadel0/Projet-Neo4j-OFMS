# Projet Neo4j-OFMS

Ce projet utilise Neo4j pour créer une base de données graphique qui modélise des transactions entre clients et distributeurs.
Actuellement, le modèle se base sur les transactions faites par les clients et les distributeurs sur les trois derniers mois.

## Configuration

Ce projet est construit avec Neo4j, et utilise la langue de requête Cypher pour manipuler les données. Assurez-vous que Neo4j est correctement installé et configuré sur votre système avant de continuer.

### Prérequis

- Neo4j Desktop
- Java 11 ou supérieur (requis pour Neo4j)

### Installation

Vous devez avoir la dernière version de Neo4j Desktop installée sur votre ordinateur ou si vous le voulez, utiliser Neo4j Aura qui vous offre une expérience sur votre navigateur.

 Lien d'installation Neo4j Desktop : [Neo4j Desktop](https://neo4j.com/download/)
 Lien Neo4j Aura : [Aura](https://login.neo4j.com/u/login/identifier?state=hKFo2SBRZHhlUFQ5dXVyaWd4NkFwcVJYWnUtUm9TODZvYXNhbaFur3VuaXZlcnNhbC1sb2dpbqN0aWTZIHBuMFV1eFFhZjlhZ2docUE2R3puYkZOTXMzbTBlNXBSo2NpZNkgV1NMczYwNDdrT2pwVVNXODNnRFo0SnlZaElrNXpZVG8)
 
### Démarrer avec Neo4j :
Une fois l'installation effectué, vous pouvez suivre ces étapes pour créer votre premier projet Neo4j:
**1.Création de projet**
Pour créer un projet neo4j vous devez d'abord cliquer sur : 
- New
- Ensuite **Create Project**

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/99d5d21a-d851-4238-a9ea-5f69f79ceab7)

Vous allez être redirigé directement vers cette page :

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/41580665-db57-4571-9ee0-49ca15c3b41e)
Pour ajouter une nouvelle base, il faut cliquez sur :
- Add,
- Ensuite : Local DBMS si vous voulez utiliser Neo4j localement
- Cliquer sur Remote connection si vous préferez utiliser Aura DB

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/c765d3e0-d47a-4422-bebe-db1e19faf99b)

Cliquez sur start pour activer la base de données, ensuite sur la flêchette à côté du bouton ouvrir pour choisir si vous 
voulez ourir : Neo4j browser, Neo4j bloom, Neo4j ETL Tool ou le terminal.
Dans un premier temps, nous allons nous intéresser au Neo4j browser.

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/59e2b4bb-78e1-47fa-8e79-20bdf5070934)

Pour importer les données et configurer la base de données, exécutez les scripts Cypher situés dans le dossier /scripts.

Exemple de script
cypher
Copy code
// Créer les noeuds Clients
LOAD CSV FROM 'file:///data/clients.csv' AS line
CREATE (:Client { name: line[0], id: line[1] });

// Créer les noeuds Distributeurs
LOAD CSV FROM 'file:///data/distributors.csv' AS line
CREATE (:Distri { name: line[0], id: line[1] });
Contribuer
Les contributions à ce projet sont bienvenues. Veuillez consulter CONTRIBUTING.md pour plus de détails sur comment contribuer au projet.

Licence
Ce projet est distribué sous la Licence MIT. Voir le fichier LICENSE pour plus d'informations.
