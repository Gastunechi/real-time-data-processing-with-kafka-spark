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
         Le code java du producteur est fournit dans le repo dans le fichier SimpleConsumer.java
     
     Compiler et exécuter le consommateur :
      ```sh
         javac -cp "$KAFKA_HOME/libs/*" SimpleConsumer.java
         java -cp "$KAFKA_HOME/libs/*:." SimpleConsumer Hello-Kafka
      ```

   7. Intégration de Kafka avec Spark
      Créer un projet Maven dans votre IDE et configurer le pom.xml pour inclure les dépendances Kafka et Spark. la configuration est fournie dans le fichier pom.xml du repo.
      Créer le package tn.insat.tp3 et la classe SparkKafkaWordCount. le fichier java SparkKafkaWordCount.java se trouve a l'interieur de stream-kafka-spark\src\main\java\spark\kafka
      Utiliser Maven pour compiler et assembler le projet.
      ```sh
         mvn clean compile assembly:single
      ```
      Copier le fichier JAR généré dans le conteneur Docker et exécuter l'application Spark avec spark-submit.
      ```sh
         docker cp target/stream-kafka-spark-1-jar-with-dependencies.jar hadoop-master:/root
      ```
      Lancer l'Application Spark
      ```sh
         Commande : spark-submit --class tn.insat.tp3.SparkKafkaWordCount --master local[2] stream-kafka-spark-1-jar-with-dependencies.jar localhost:2181 test Hello-Kafka 1 >> out
   







# real-time-data-processing-with-kafka-spark
Project to integrate Kafka with Spark Streaming for real-time data processing / Projet d'intégration de Kafka avec Spark Streaming pour le traitement des données en temps réel 

# Real-time Data Processing with Kafka and Spark

## Description

This project shows how to integrate Apache Kafka with Apache Spark Streaming for real-time data processing. Kafka acts as a central hub for real-time data streams, which are then processed with Spark Streaming. Once the data has been processed, it can be published in another Kafka topic or stored in HDFS, other databases, or visualized in dashboards.

## Prerequisites

- [Docker](https://www.docker.com/get-started)
- Kafka](https://kafka.apache.org/)
- [Spark](https://spark.apache.org/)
- Java](https://www.oracle.com/java/technologies/javase-downloads.html)
- [Maven](https://maven.apache.org/)

## Installation

1. Clone this repository:
   ``sh
   git clone https://github.com/votre-utilisateur/real-time-data-processing-with-kafka-spark.git
   cd real-time-data-processing-with-kafka-spark
   
2. Start Docker containers for Kafka and Zookeeper:
   docker start hadoop-master hadoop-slave1 hadoop-slave2
   docker exec -it hadoop-master bash
   ./start-hadoop.sh
   ./start-kafka-zookeeper.sh


4. Check that the Kafka and Zookeeper daemons are running :
   jps

5. Using Kafka
  Creating a topic
  ```sh
     kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic Hello-Kafka
  ```
  List of existing topics

  Example Producer
  ```sh
  kafka-console-producer.sh --broker-list localhost:9092 --topic Hello-Kafka

  ```
  Example Consumer
  
    kafka-console-consumer.sh --zookeeper localhost:2181 --topic Hello-Kafka --from-beginning

  6. Customized application
     Personalized producer:
       The personalized Kafka producer sends 10 sequentially numbered messages (from 0 to 9) to a specified Kafka topic. The producer's java code is provided on the repo in the file SimpleProducer.java .this file must be created in the hadoop-master Docker container.
     Compile and run the producer :
       ```sh
         javac -cp "$KAFKA_HOME/libs/*" SimpleProducer.java
         java -cp "$KAFKA_HOME/libs/*:." SimpleProducer Hello-Kafka
      ```
       Customized consumer:
         The java code of the producer is provided in the repo in the file SimpleConsumer.java
     
     Compile and run the consumer :
      ```sh
         javac -cp "$KAFKA_HOME/libs/*" SimpleConsumer.java
         java -cp "$KAFKA_HOME/libs/*:." SimpleConsumer Hello-Kafka
      ```


   7. Integrating Kafka with Spark
      Create a Maven project in your IDE and configure the pom.xml to include Kafka and Spark dependencies. The configuration is provided in the pom.xml file on the repo.
      Create the tn.insat.tp3 package and the SparkKafkaWordCount class. The SparkKafkaWordCount.java file can be found inside stream-kafka-spark\smainjava\spark\kafka
      Use Maven to compile and assemble the project.
      ```sh
         mvn clean compile assembly:single
      ```
      Copy the generated JAR file into the Docker container and run the Spark application with spark-submit.
      ```sh
         docker cp target/stream-kafka-spark-1-jar-with-dependencies.jar hadoop-master:/root
      ```
      Launch Spark Application
      ```sh
         Command: spark-submit --class tn.insat.tp3.SparkKafkaWordCount --master local[2] stream-kafka-spark-1-jar-with-dependencies.jar localhost:2181 test Hello-Kafka 1 >> out
