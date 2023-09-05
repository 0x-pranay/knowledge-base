### Apache kafka









```bash
$ docker run -p 9092:9092 apache/kafka:3.8.0
```





```
kafka-topics.sh --bootstrap-server localhost:9092 --topic globalPortalNotifications --create --partitions 3 --replication-factor 1
```









----------------------------





https://www.conduktor.io/kafka/kafka-topics-cli-tutorial/

https://www.conduktor.io/kafka/how-to-install-apache-kafka-on-linux/





----



https://medium.com/inspiredbrilliance/kafka-basics-and-core-concepts-5fd7a68c3193

- Distributed
- event streaming platform
- uses tcp network protocol
- producer and consumers are decoupled



Kafka's performance is effectively constant wrt data size. 







1. One partition in a topic will always push messages to a single consumer in a consumer group. 

2. One consumer in a consumer group can pull messages from one or more partitions in a topic.

   =









#### Use cases:

- Messaging - alt to ActiveMQ or RabbitMQ
- Metrics - aggregateing statistics from distributed application to produce centralised feed
- Log aggregation - collects physcial log files off servers and puts in a centralised place
- Stream processing - data processsing pipelines ( lightweight library - __Kafka stream__). alts - apache storm and apache samza
- Event Sourcing - excellent for backend  for an application designed on where state changes are logged as a time-ordered sequence of records
- Commit log - external commit log for a distributed system. Look at **log compaction** feature in kafka
- 



#### kafka Guarantees:

Semantic guarantees kafka provides between producer and consumer

- _At most once_ - Messages may be lost but are never redelivered.

- _At least once_ - Messages are never lost but may be redelivered.

- _Exactly once_ - Each message delivered only once.

  



#### Producers

Clients that publish or write to Kafka.





#### Consumers





#### Topics:

Events are organised and durably stored in *topics*.

Topics are always multi-producers and multi -subscribers.

__per topic configuration__ of events, meaning events are not deleted after consumption, we can define for how long kafka should retain those events.

Topics are __partitioned__ over different kafka brokers.

To make data fault-tolerant and Highly available, every topic can be __replicated__







- Produce and consume a stream of data records
- high accuracy and fast
- in-order
- fault tolerant







4 Core api's

- Producer API
- Consumer API- subscribes to topic
- Streams API- to analyse, aggrege and transform the data
- connector API