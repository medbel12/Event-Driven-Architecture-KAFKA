# Kafka Project README

## Introduction

This project demonstrates how to set up and use Apache Kafka, both manually and with Docker, alongside Spring Cloud Streams to create a data analytics application.

## Table of Contents

1. [Setup Kafka Manually](#setup-kafka-manually)
2. [Setup Kafka Using Docker](#setup-kafka-using-docker)
3. [Creating Services with Spring Cloud Streams](#creating-services-with-spring-cloud-streams)

## 1. Setup Kafka Manually

Follow these steps to set up Kafka manually:

### Step 1: Download Kafka

- Download Apache Kafka from the [official website](https://kafka.apache.org/downloads).

### Step 2: Start Zookeeper

- Navigate to the Kafka directory and run the following command to start Zookeeper:
  ```bash
  bin/zookeeper-server-start.sh config/zookeeper.properties
  ```

### Step 3: Start Kafka Server

- In another terminal window, navigate to the Kafka directory and start the Kafka server:
  ```bash
  bin/kafka-server-start.sh config/server.properties
  ```

### Step 4: Test with Kafka Console Producer and Consumer

- To test the setup, use the following commands:

  **Start the Console Producer**:
  ```bash
  bin/kafka-console-producer.sh --topic test --bootstrap-server localhost:9092
  ```

  **Start the Console Consumer**:
  ```bash
  bin/kafka-console-consumer.sh --topic test --from-beginning --bootstrap-server localhost:9092
  ```

## 2. Setup Kafka Using Docker

Alternatively, you can set up Kafka using Docker. For more detailed instructions, you can refer to the [Confluent Kafka Docker Quickstart](https://developer.confluent.io/quickstart/kafka-docker/) or this [YouTube tutorial](https://www.youtube.com/watch?v=9O1Kuk2xXO8).

### Step 1: Create the Docker Compose File

- Create a `docker-compose.yml` file with the following content:
  ```yaml
  version: '2'
  services:
    zookeeper:
      image: wurstmeister/zookeeper:3.4.6
      ports:
        - "2181:2181"
    kafka:
      image: wurstmeister/kafka:latest
      ports:
        - "9092:9092"
      environment:
        KAFKA_ADVERTISED_LISTENERS: INSIDE://kafka:9092,OUTSIDE://localhost:9092
        KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: INSIDE:PLAINTEXT,OUTSIDE:PLAINTEXT
        KAFKA_LISTENERS: INSIDE://0.0.0.0:9092,OUTSIDE://0.0.0.0:9092
        KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
  ```

### Step 2: Start the Docker Containers

- Run the following command to start the Zookeeper and Kafka broker containers:
  ```bash
  docker-compose up -d
  ```

### Step 3: Test with Kafka Console Producer and Consumer

- Similar to the manual setup, you can test using the console producer and consumer:
  
  **Start the Console Producer**:
  ```bash
  docker exec -it <kafka-container-name> kafka-console-producer --topic test --bootstrap-server localhost:9092
  ```

  **Start the Console Consumer**:
  ```bash
  docker exec -it <kafka-container-name> kafka-console-consumer --topic test --from-beginning --bootstrap-server localhost:9092
  ```

## 3. Creating Services with Spring Cloud Streams

Using Kafka and Spring Cloud Streams, you can create various services for your application:

### Step 1: Create a Kafka Producer Service via a REST Controller

- Implement a REST controller that publishes messages to a Kafka topic.

### Step 2: Create a Kafka Consumer Service

- Develop a service that consumes messages from a Kafka topic.

### Step 3: Create a Kafka Supplier Service

- Create a supplier service that provides messages to Kafka.

### Step 4: Create a Real-Time Data Analytics Service

- Implement a service for real-time stream processing using Kafka Streams.

### Step 5: Develop a Web Application

- Build a web application that displays the results of the stream data analytics in real-time.

## Conclusion

This README provides a comprehensive guide to setting up Kafka manually or using Docker and integrating it with Spring Cloud Streams for building a real-time data analytics application. Follow the steps outlined above to get your application up and running!
