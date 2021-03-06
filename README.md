Apache Kafka with sample Kafka Connect connector
===
Kafka, Zookeeper and maven (in order to compile Kafka Connect connectors) in a single Docker

Nothing else is needed to run a single Kafka broker.

Quickstart
---
**Scenario**

Move only 'body' parts of the messages from RabbitMQ to Kafka topic. Optional step - read messages from kafka topic and display them on your terminal screen.

**Step-by-step guide**

Copy config files from `/sample_config` directory to your `/host/volume`. Adjust settings to meet your needs. Don't forget to set  `advertised.host.name` at the bottom of the `server.properties` file.

Run docker with config files from your /host/volume 
```bash
docker run -dt -v /host/volume:/opt/kafka_2.11-0.10.2.0/config/ --name my_kafka -p 2181:2181 -p 9092:9092 lmurawsk/kafka:10.2
```

Log in to the container:
```bash
docker exec -it my_kafka bash
```

Go to Kafka home directory:
```bash
cd $KAFKA_HOME
``` 

Start RabbitMQ connector (thanks to https://github.com/jcustenborder/kafka-connect-rabbitmq):
```bash
./bin/connect-standalone.sh config/connect-standalone.properties config/RabbitMQSourceConnector.properties
```

**Optionally**

To display those messages in you console, start a consumer:
```bash
./bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topic_name --from-beginning
```
Parameters
---
For more details ragarding Kafka docker parameters please refer to the spotify repo: https://github.com/spotify/docker-kafka

Public Builds
---

https://hub.docker.com/r/lmurawsk/kafka/
