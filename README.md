# kafka_with_docker


## Docker Compose File

version: "2"

services:
  kafkaserver:
    image: "spotify/kafka:latest"
    container_name: kafka
    hostname: kafkaserver
    networks:
      - kafkanet
    ports:
      - 2181:2181
      - 9092:9092
    environment:
      ADVERTISED_HOST: kafkaserver
      ADVERTISED_PORT: 9092
  kafka_manager:
    image: "mzagar/kafka-manager-docker:1.3.3.4"
    container_name: kafkamanager
    networks:
      - kafkanet
    ports:
      - 9000:9000
    links:
      - kafkaserver
    environment:
      ZK_HOSTS: "kafkaserver:2181"

networks:
  kafkanet:
    driver: bridge




