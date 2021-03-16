# Quick Start

> [Offical Documentation](https://kafka.apache.org/documentation)

## Pre-requisite

* Install [Java 8+](https://openjdk.java.net/install/)

## Preparation

1. [Download](https://kafka.apache.org/downloads) and unzip the latest Kafka.

2. Start the Zookeeper service.

   ```sh
   bin/zookeeper-server-start.sh config/zookeeper.properties
   ```

## Setup

### Single Node, Single Broker

1. Start the Kafka broker.

   ```sh
   bin/kafka-server-start.sh config/server.properties
   ```

2. Manage the topics.

   ```sh
   # Create the topic.
   bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic single-broker-demo --replication-factor 1 --partitions 1

   # Describe the topic.
   bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic single-broker-demo

   # List all the topics.
   bin/kafka-topics.sh --bootstrap-server localhost:9092 --list
   ```

3. Write some events into the topic.

   ```sh
   bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic single-broker-demo
   ```

   Separate lines are sent as separate events. Press `Ctrl-C` to quit the program.

4. Read the events.

   ```sh
   bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic single-broker-demo --from-beginning
   ```

   Press `Ctrl-C` to quit the program.

5. Stop the Kafka broker.

   ```sh
   bin/kafka-server-stop.sh
   ```

### Single Node, Multiple Brokers

1. Copy `config/server.properties` as `config/server.a.properties`, `config/server.b.properties` and `config/server.c.properties`.

2. Update the corresponding lines in the property files.

   `config/server.a.properties`

   ```
   broker.id=0
   listeners=PLAINTEXT://localhost:9092
   log.dirs=/tmp/kafka-logs.a
   ```

   `config/server.b.properties`

   ```
   broker.id=1
   listeners=PLAINTEXT://localhost:9093
   log.dirs=/tmp/kafka-logs.b
   ```

   `config/server.c.properties`

   ```
   broker.id=2
   listeners=PLAINTEXT://localhost:9094
   log.dirs=/tmp/kafka-logs.c
   ```

   **NOTE**: If you setup the brokers on separate nodes, you might bind the listener to the `0.0.0.0` interface for example. In this case, you need to configure [advertised.listeners](https://kafka.apache.org/documentation/#brokerconfigs_advertised.listeners) as well.

3. Start the brokers (in separate terminals).

   ```sh
   # Broker A
   bin/kafka-server-start.sh config/server.a.properties
   # Broker B
   bin/kafka-server-start.sh config/server.b.properties
   # Broker C
   bin/kafka-server-start.sh config/server.c.properties
   ```

4. Since we have 3 brokers, we can create the topic with the replication factor of `3`, so that each partition will have 1 leader and 2 extra replicas.

   ```sh
   # Create the topic.
   bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic multi-broker-demo --replication-factor 1 --partitions 1

   # Describe the topic.
   bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic multi-broker-demo

   # List all the topics.
   bin/kafka-topics.sh --bootstrap-server localhost:9092 --list
   ```

5. You should see a similar output when you describe the topic.

   ```
   Topic: multi-broker-demo	PartitionCount: 1	ReplicationFactor: 3	Configs:
	   Topic: multi-broker-demo	Partition: 0	Leader: 2	Replicas: 2,0,1	Isr: 2,0,1
   ```

   The first line shows the topic configuration that we have provided.

   The second line shows that partition `0` is led by broker `2`. The replicas are expected to be found on brokers `2`, `0` and `1`. **Isr** indicates the set of in-sync brokers.

6. Play around with the producer and consumer scripts.

7. Stop the Kafka brokers.

   ```sh
   bin/kafka-server-stop.sh
   ```

## Clean up

```sh
rm -rf /tmp/kafka-logs /tmp/zookeeper
```
