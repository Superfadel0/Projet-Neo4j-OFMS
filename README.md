# Projet Neo4j-OFMS

Ce projet utilise Neo4j pour créer une base de données graphique qui modélise des transactions entre clients et distributeurs. Actuellement, le modèle se base sur les transactions effectuées par les clients et les distributeurs au cours des trois derniers mois.

## Configuration

Ce projet est construit avec Neo4j et utilise le langage Cypher pour manipuler les données. Avant de continuer, assurez-vous que Neo4j est correctement installé et configuré sur votre système.

### Prérequis

- Neo4j Desktop
- Java 11 ou supérieur (requis pour Neo4j)

### Installation

Vous pouvez installer la dernière version de Neo4j Desktop sur votre ordinateur, ou si vous préférez, utiliser Neo4j Aura, qui offre une expérience directement dans votre navigateur.

 Lien d'installation Neo4j Desktop : [Neo4j Desktop](https://neo4j.com/download/)
 Lien Neo4j Aura : [Aura](https://login.neo4j.com/u/login/identifier?state=hKFo2SBRZHhlUFQ5dXVyaWd4NkFwcVJYWnUtUm9TODZvYXNhbaFur3VuaXZlcnNhbC1sb2dpbqN0aWTZIHBuMFV1eFFhZjlhZ2docUE2R3puYkZOTXMzbTBlNXBSo2NpZNkgV1NMczYwNDdrT2pwVVNXODNnRFo0SnlZaElrNXpZVG8)
 
### Démarrer avec Neo4j :
Une fois l’installation effectuée, suivez ces étapes pour créer votre premier projet Neo4j :
**1.Création du projet :**
Cliquez sur “New”, puis “Create Project”.

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/99d5d21a-d851-4238-a9ea-5f69f79ceab7)

Vous serez redirigé vers cette page où vous pourrez ajouter une base de données :

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

On veut importer le fichier transaction_intouch dans neo4j. Pour ce faire, il faut créer les noeuds correspondants (sender et receiver) ansi que la relation qui les lie :


```LOAD CSV WITH HEADERS FROM 'file:///transaction_intouch.csv' as row
// Créer ou fusionner les nœuds de sender et receiver

// Creation noeud sender avec ses propriétés
MERGE (sender:Sender {id: row.sender})
  ON CREATE SET 
  sender.sender = row.sender,
  sender.commissions_paid = toInteger(row.COMMISSIONS_PAID),
  sender.SENDER_USER_ID = row.SENDER_USER_ID


// Creation du noeud receiver avec ses propriétés
MERGE (receiver:Receiver {id: row.sim_intouch})
  ON CREATE SET 
  receiver.sim_intouch = row.sim_intouch,
  receiver.receiver_domain_code = row.RECEIVER_DOMAIN_CODE, 
  receiver.first_name = row.first_name

// Création de la relation TRANSACTION entre les sender et les receiver
MERGE (sender)-[:TRANSACTION {
    date_transaction: row.date_transaction,
    MNT_TRANSACTION: toInteger(row.MNT_TRANSACTION),
    SERVICE_TYPE: row.SERVICE_TYPE,
    TRANSACTION_TAG: row.TRANSACTION_TAG
}]->(receiver)
```

Si vous avez une grande quantité de données, je vous conseillerai d'ajouter des index pour optimiser le temps d'exécution :

```
CREATE INDEX FOR (s:Sender) ON (s.id);
CREATE INDEX FOR (r:Receiver) ON (r.id);
```














![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/a7d1b341-bcf6-4461-bc35-0c5e3b987345)



