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
 
3. **Démarrer avec Neo4j :**
Une fois l'installation effectué, vous pouvez suivre ces étapes pour créer votre premier projet Neo4j
![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/99d5d21a-d851-4238-a9ea-5f69f79ceab7)

Structure du projet
/data : Contient les fichiers CSV utilisés pour l'importation de données.
/scripts : Scripts Cypher pour la création de noeuds, de relations et d'indices.
/docs : Documentation du projet, y compris les spécifications et les manuels d'utilisation.
Utilisation
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