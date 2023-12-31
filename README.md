## Apache Kafka example

Apache Kafka is a framework implementation of a event bus using stream-processing.

Kafka in microservices is a messaging platform that enables different microservices to communicate and share data in a scalable and casually connected manner( not tightly ie,it is more flexible and informal, allowing services to interact as needed without strict constraints), facilitating real-time data flow between services.

Kafka's architecture is based on distributed publish-subscribe(pub-sub) messaging, where producers send messages to topics, which are divided into partitions and managed by brokers, with consumers subscribing to and reading messages from these partitions.

 ZooKeeper used to be like a supervisor for Kafka, making sure everything runs smoothly,

 <img src="https://res.cloudinary.com/dn8sdjsfn/image/upload/v1695993761/kafka/1_mlpnba.png" width="900"><br>
 <img src="https://res.cloudinary.com/dn8sdjsfn/image/upload/v1695993762/kafka/2_mhqujj.png" width="900"><br>
 <img src="https://res.cloudinary.com/dn8sdjsfn/image/upload/v1695993762/kafka/3_lblt61.png" width="900"><br>
 <img src="https://res.cloudinary.com/dn8sdjsfn/image/upload/v1695993763/kafka/4_hxtokd.png" width="900"><br>
 its a replica set. Read/write operations are performed on leader. then changes are replicated to other followers.
 
 <img src="https://res.cloudinary.com/dn8sdjsfn/image/upload/v1695993764/kafka/5_h0zrh2.png" width="900"><br>
 <img src="https://res.cloudinary.com/dn8sdjsfn/image/upload/v1695993763/kafka/6_a5ontc.png" width="900"><br>

3 Main Entities:
  - Topic: Space where data is produces and consumed.
  - Producer: Produces data to topic.
  - Consumer: Consumes data from topic.

  ### steps

  - Install Docker (if not installed)

  - pull and Start Zookeper Container and expose PORT 2181

  ```
    docker run -p 2181:2181 zookeeper
  ```

  - Start Kafka Container, expose PORT 9092 and setup ENV variables.

  // to get KAFKA_ZOOKEEPER_CONNECT privete ip (in which zookeeper is running)

  ```
    docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <zookeeper container id>
  ```

  ```
  docker run -p 9092:9092 \
    -e KAFKA_ZOOKEEPER_CONNECT=<PRIVATE_IP>:2181 \
    -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://<localhost or localhost ip>:9092 \
    -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 confluentinc/cp-kafka
  ```

  - Open Project in VS code and run

  ```
    node partition.js
    node producer.js hello
    node consumer.js
  ```
