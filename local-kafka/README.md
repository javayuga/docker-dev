# docker-dev
Docker-based services to be used in development


## Kafka

Kafka containers for development, provided as docker-compose services

Available at **local-kafka** folder

### Services

Three services are provided within **local-kafka** network:

- [Kafka](https://kafka.apache.org/) Message Broker
- [Kafdrop](https://hub.docker.com/r/obsidiandynamics/kafdrop) (manager UI)
- [Zookeeper](https://zookeeper.apache.org/) (centralized configuration and monitoring)

### How to use

```
> cd c:\pub\multicanal-docker\local-kafka
> docker-compose up
...
wait for image pull on first run
...

```

Depending on your version of Docker, and the amount of available RAM, occasionally you might run into trouble trying to start containers.

Please try starting services individually, according to this order: zookeeper >> kafka >> kafdrop.


To access Kafdrop:
[http://localhost:19000/](http://localhost:19000/)

#### KAFKA CLI (via Docker)

Connect to Kafka service, then verify version:

```
> C:\pub\multicanal-docker\local-kafka
> docker-compose kafka bash
> [appuser@8ede5f2e40e6 ~]$$KAFKA_HOME/bin/kafka-dump-log --version

```

Similarly, you may use other Kafka CLI commands

For instance, to create a topic:

```
[appuser@8ede5f2e40e6 ~]$ $KAFKA_HOME/bin/kafka-topics -zookeeper zookeeper:2181 --create --topic first-topic --partitions 3 --replication-factor 1
Created topic first-topic.
```

### Kafdrop

Topics can be created/dropped/eavesdropped via Kafdrop UI.

To [visualize first-topic in Kafdrop](http://localhost:19000/topic/first-topic)

[Endpoints defined on swagger](http://localhost:19000/v2/api-docs)


### Images

[confluentinc/cp-kafka](https://hub.docker.com/r/confluentinc/cp-kafka/)

[obsidiandynamics/kafdrop](https://github.com/obsidiandynamics/kafdrop)

[confluentinc/cp-zookeeper](https://hub.docker.com/r/confluentinc/cp-zookeeper)

### References

[Kafka documentation](https://kafka.apache.org/documentation/)

[Kafka CLI cheatsheet](https://medium.com/@TimvanBaarsen/apache-kafka-cli-commands-cheat-sheet-a6f06eac01b)



