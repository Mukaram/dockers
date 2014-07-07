Dockers
=======

A repository to maintain Dockerfiles for building containers of : Kafka, Storm, Zookeeper


Build the containers locally by running the docker build command:
docker build -t mukaram\zookeeper:3.4.5 --no-cache .
docker build -t mukaram/kafka:0.8.1 --no-cache .
docker build -t mukaram/stormbase:0.9.2 --no-cache .
docker build -t mukaram/storm-nimbus:0.9.2 --no-cache .
docker build -t mukaram/storm-node:0.9.2 --no-cache .
docker build -t mukaram/storm-ui:0.9.2 --no-cache .


Manually run these commands to start up a cluster. A single script to instantiate a cluster is being worked on.

Zookeeper (run this first)
docker run -p 49181:2181  -h zookeeper --name zookeeper -d mukaram/zookeeper

3-node Kafka cluster
docker run -p 9092:9092 --link zookeeper:zk -e BROKER_ID=1 -e HOST_IP=<<host IP>> -e PORT=9092 -d mukaram/kafka:0.8.1
docker run -p 9093:9093 --link zookeeper:zk -e BROKER_ID=2 -e HOST_IP=<<host IP>> -e PORT=9093 -d mukaram/kafka:0.8.1
docker run -p 9094:9094 --link zookeeper:zk -e BROKER_ID=3 -e HOST_IP=<<host IP>> -e PORT=9094 -d mukaram/kafka:0.8.1

Consume and produce 
$KAFKA_HOME/bin/kafka-console-producer.sh --broker-list <<host IP>>:9092 --topic test
$KAFKA_HOME/bin/kafka-console-consumer.sh --zookeeper $ZK_PORT_2181_TCP_ADDR:2181 --topic test --from-beginning


1-node Storm cluster. To increase the number of nodes, run the storm-node container as many times by changing the port number
docker run -p 49773:3773 -p 49772:3772 -p 49627:6627 --name nimbus --link zookeeper:zk -h nimbus -d mukaram/storm-nimbus:0.9.2
docker run -p 49000:8000 --name supervisor --link nimbus:nimbus --link zookeeper:zk -h supervisor -d mukaram/storm-node:0.9.2
docker run -p 49080:8080 --name ui --link nimbus:nimbus --link zookeeper:zk -d mukaram/storm-ui:0.9.2

On Mac/Boot2Docker setup, host IP is obtained by running  "boot2docker ip" command