Quarkus Kafka Quickstart
========================

This project illustrates how you can interact with Apache Kafka using MicroProfile Reactive Messaging.

## Kafka cluster

###Hervorragendes Indisches Tutorial:
https://www.youtube.com/watch?v=NjHYWEV_E_o
https://www.youtube.com/watch?v=IncG0_XSSBg

###Kafka Download:
https://kafka.apache.org/downloads

###Steps:
1. Start zookeeper ./bin/zookeeper-server-start.sh config/zookeeper.properties
2. Start kafka ./bin/kafka-server-start.sh config/server.properties
3. Create Topic ./bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic prices

## Start the application

The application can be started using: 

```bash
mvn quarkus:dev
```  

Then, open your browser to `http://localhost:8080/prices.html`, and you should see a fluctuating price.

## Anatomy

In addition to the `prices.html` page, the application is composed by 3 components:

* `PriceGenerator` - a bean generating random price. They are sent to a Kafka topic
* `PriceConverter` - on the consuming side, the `PriceConverter` receives the Kafka message and convert the price.
The result is sent to an in-memory stream of data
* `PriceResource`  - the `PriceResource` retrieves the in-memory stream of data in which the converted prices are sent and send these prices to the browser using Server-Sent Events.

The interaction with Kafka is managed by MicroProfile Reactive Messaging.
The configuration is located in the application configuration.

## Running in native

You can compile the application into a native binary using:

`mvn clean install -Pnative`

and run with:

`./target/kafka-quickstart-1.0-SNAPSHOT-runner` 