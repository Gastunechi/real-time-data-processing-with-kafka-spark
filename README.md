# real-time-data-processing-with-kafka-spark
Projet d'intégration de Kafka avec Spark Streaming pour le traitement des données en temps réel / Project to integrate Kafka with Spark Streaming for real-time data processing 

# Real-time Data Processing with Kafka and Spark

## Description

Ce projet montre comment intégrer Apache Kafka avec Apache Spark Streaming pour traiter des données en temps réel. Kafka agit comme un hub central pour les flux de données en temps réel qui sont ensuite traités avec Spark Streaming. Une fois les données traitées, elles peuvent être publiées dans un autre topic Kafka ou stockées dans HDFS, d'autres bases de données, ou visualisées dans des dashboards.

## Prérequis

- [Docker](https://www.docker.com/get-started)
- [Kafka](https://kafka.apache.org/)
- [Spark](https://spark.apache.org/)
- [Java](https://www.oracle.com/java/technologies/javase-downloads.html)
- [Maven](https://maven.apache.org/)

## Installation

1. Cloner ce dépôt :
   ```sh
   git clone https://github.com/votre-utilisateur/real-time-data-processing-with-kafka-spark.git
   cd real-time-data-processing-with-kafka-spark
   
2. Démarrer les conteneurs Docker pour Kafka et Zookeeper :
   docker start hadoop-master hadoop-slave1 hadoop-slave2
   docker exec -it hadoop-master bash
   ./start-hadoop.sh
   ./start-kafka-zookeeper.sh


4. Vérifier que les démons Kafka et Zookeeper sont lancés :
   jps

5. Utilisation de Kafka
  Création d'un topic
  ```sh
     kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic Hello-Kafka
  ```
  Liste des topics existants

  Exemple Producteur
  ```sh
  kafka-console-producer.sh --broker-list localhost:9092 --topic Hello-Kafka

  ```
  Exemple Consommateur
  
    kafka-console-consumer.sh --zookeeper localhost:2181 --topic Hello-Kafka --from-beginning

  6. Application personalisée
     Producteur personalisé:
       Le producteur personalise Kafka envoie 10 messages numérotés séquentiellement (de 0 à 9) à un topic Kafka spécifié. Le code java du producteur est fournit dans le repo dans le fichier SimpleProducer.java .ce fichier doit etre cree dans le contenaire Docker hadoop-master.
     Compiler et exécuter le producteur :
       ```sh
         javac -cp "$KAFKA_HOME/libs/*" SimpleProducer.java
         java -cp "$KAFKA_HOME/libs/*:." SimpleProducer Hello-Kafka
      ```
       Consommateur personalisé:
     

   

