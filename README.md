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
Créez un nouveau projet en cliquant sur "New", puis "Create Project".

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/99d5d21a-d851-4238-a9ea-5f69f79ceab7)

Vous serez dirigé vers une page où vous pourrez ajouter une base de données. 
![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/41580665-db57-4571-9ee0-49ca15c3b41e)

Pour cela :
* Cliquez sur "Add".
* Choisissez "Local DBMS" pour utiliser Neo4j localement ou "Remote connection" pour utiliser Aura DB.


![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/c765d3e0-d47a-4422-bebe-db1e19faf99b)

Activez la base de données en cliquant sur "start", puis utilisez le menu à côté du bouton "ouvrir" pour choisir entre Neo4j Browser, Neo4j Bloom, Neo4j ETL Tool ou le terminal.
![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/77f9f9e7-9bd4-4060-81f3-f36ceb057f24)


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

RESULTAT :

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/77de6148-0efc-46c9-b723-f52a6558d66b)

VISUALISATION :

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/04633c5e-8af1-46fb-8820-b1f7566a5eea)


# UTILISATION DE NEO4J BLOOM

Neo4j Bloom est une application de visualisation graphique conçue pour faciliter l'exploration intuitive et la compréhension des graphes stockés dans Neo4j. Bloom permet aux utilisateurs, qu'ils soient analystes, data scientists ou développeurs, de visualiser les données de manière interactive sans nécessiter de compétences approfondies en langage de requête graphique. Voici quelques-unes de ses principales caractéristiques :

  ### Visualisation Intuitive : 
  Bloom fournit une représentation visuelle des nœuds, des relations et des propriétés qui aide à comprendre les interconnexions complexes au sein des données.

  ### Recherche par Perspective : 
  Les utilisateurs peuvent créer et utiliser des "perspectives" qui configurent comment les différents types de nœuds et de relations sont visualisés et interagissent. Cela permet de personnaliser la        vue du graphe selon les besoins spécifiques de l'utilisateur ou du projet.

  ### Requêtes Naturelles : 
  Avec le langage de recherche basé sur le langage naturel, les utilisateurs peuvent explorer le graphe en posant des questions simples en anglais, sans nécessiter la maîtrise du Cypher.

  ### Outils de Collaboration : 
  Bloom permet de partager des visualisations et des découvertes au sein d'une équipe, facilitant ainsi la collaboration sur des projets basés sur des graphes.

  ### Interactivité : 
  Les utilisateurs peuvent zoomer, faire pivoter, et explorer les détails des nœuds et des relations, ce qui rend l'analyse des graphes à la fois engageante et détaillée.
![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/a7d1b341-bcf6-4461-bc35-0c5e3b987345)




![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/1d0f820a-d544-4de3-9f86-0119ac6c0fe9)



## Recherche de motifs de graphe


Pour créer des modèles de graphe, vous pouvez utiliser les suggestions proactives de Bloom dans Neo4j. Cette fonction vous aide à choisir des éléments de votre schéma, comme les types de relations ou les connexions entre catégories. Dans la barre de recherche de Bloom, vous trouverez des options pour démarrer vos recherches, choisir des étiquettes de nœuds, ou sélectionner des relations et filtrer par des critères spécifiques.

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/46674a5a-0d95-49de-8771-2b6a95314d9f)


Si vous sélectionnez une étiquette de nœud, par exemple, Bloom vous permet de choisir si vous souhaitez filtrer davantage le nœud de départ en fonction de ses relations ou si vous souhaitez affiner par propriétés et/ou valeurs de propriété. Bloom vous donne un indice sur le type de données de la valeur de la propriété directement dans la barre de recherche.


![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/f9af0737-cf37-44a2-b091-a7b3e2955a0f)

## Slicer

Le Slicer est une fonctionnalité qui vous permet de modifier rapidement et de manière interactive ce qui est visible dans votre scène. Il vous permet de démontrer la différence dans les valeurs numériques des propriétés via une chronologie. Vous pouvez le faire en faisant défiler manuellement ou en utilisant la fonction de lecture.

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/0c74ef90-e5b1-4679-8ce0-50bef93ddb22)


Dans l'exemple ci-dessous, j'essaie d'afficher les transactions comprises entre 203 et 393 FCFA. Elles sont au nombre de 8.

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/7cf5ae96-7029-48c2-a1a1-061a6ecc5fa5)

## Graph Data Science integration
Cette partie est pour moi la plus exaltante dans bloom. Les algorithmes de Graph Data Science peuvent vous aider à trouver de nouvelles informations dans vos données, à la fois sur les nœuds eux-mêmes et sur la façon dont ils sont connectés.

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/b66b4b68-6128-456a-8b81-55b598b5b17e)


Les algorithmes que Bloom propose se répartissent en deux grandes catégories : centralité et détection de communauté. Les algorithmes de centralité évaluent l'importance des nœuds dans un réseau, en mettant en lumière leur rôle. Un nœud peut être jugé important s'il possède de nombreuses connexions, s'il est lié transitivement à d'autres nœuds clés, s'il est accessible en peu de sauts, ou s'il se trouve sur le chemin le plus court entre plusieurs paires de nœuds. Voici les algorithmes de centralité disponibles dans Bloom :

* Betweenness Centrality

* Degree Centrality

* Eigenvector Centrality

* PageRank

Les algorithmes de détection de communauté dans Bloom permettent de trouver des groupes ou des clusters au sein de vos données. Cela peut vous aider à comprendre comment les différents éléments de vos données sont connectés ou isolés, ce qui est très utile dans de nombreux domaines, comme les réseaux sociaux ou l'apprentissage automatique. Ces outils identifient les sous-groupes qui partagent des caractéristiques communes ou qui sont plus fréquemment connectés entre eux. Les algorithmes de détection de fraude disponible dans Neo4j bloom sont :
* Louvain

* Label propagation

* Weakly connected components

### Louvain : 
Cet algorithme cherche à regrouper des nœuds étroitement liés dans un réseau plus large, ce qui est bénéfique, par exemple, pour des recommandations de produits.
### Label Propagation :
Cette méthode identifie des communautés en permettant une certaine supervision et contrôle sur les résultats, ce qui est avantageux quand vous disposez déjà de certaines connaissances sur la structure des données.
Composants faiblement connectés: Cet algorithme trouve des sous-graphes isolés qui ne sont pas accessibles depuis d'autres parties du réseau, utile pour vérifier la connectivité globale du réseau ou identifier des points faibles dans des chaînes d'approvisionnement.
Concernant les algorithmes de centralité disponibles dans Bloom :

### Centralité des degrés :
Cet algorithme évalue l'importance d'un nœud en comptant les connexions entrantes, sortantes ou les deux, afin d'identifier les nœuds les plus centraux dans un réseau.
### Betweenness Centrality : 
Connu sous le nom de Betweenness Centrality, cet outil identifie les nœuds qui agissent comme des ponts sur les chemins les plus courts à travers le réseau, connectant ainsi différentes parties d'un graphe.
### Eigenvector Centrality : 
Cette méthode évalue l'influence transitive des nœuds, c'est-à-dire que pour qu'un nœud soit jugé influent, il doit être connecté à d'autres nœuds qui sont eux-mêmes bien connectés.
### PageRank : 
Cette approche évalue l'importance d'un nœud basée sur le nombre de liens entrants et l'influence des nœuds qui établissent ces liens.
Chacun de ces algorithmes offre une perspective unique sur la structure et la dynamique des réseaux, permettant ainsi une analyse approfondie et ciblée en fonction des besoins spécifiques de votre projet.

### Weakly connected components :
L'algorithme Weakly connected components identifie les parties d'un graphe qui ne sont pas reliées aux autres. Cet outil est pratique pour vérifier si toutes les parties de votre réseau sont interconnectées ou pour localiser les zones fragiles dans des structures comme les chaînes d'approvisionnement.



# Gestion des erreurs

![Capture d'écran 2024-05-14 092124](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/051a06e3-6abd-4c72-8a89-d93b7b69647c)


Cette erreur indique que la procédure n'est pas spécifiée dans la base de données. Pour la résoudre, il faut :

1. Cliquer sur la base de donnée en question
2. Ensuite sur Plugins, situé à droite
3. Cliquer sur APOC
4. Enfin sur Install et Restart

![image](https://github.com/Superfadel0/Projet-Neo4j-OFMS/assets/126486272/d088d6bf-7402-4958-83ab-d5eb2c569447)


Effectué les mêmes étapes si vous rencontrez des erreurs en lien avec Graph Data Science





