# Running docker-compose
`docker-compose up` to start kafka container
`docker-compose run kafka /bin/bash` to run kafka container service iteractively

## docker related cli
to run another process in same running docker
`docker exec -it <name> /bin/bash`
to detach without shutting down container
`control-p control-q` 

# Config
config/zookeeper.properties
config/kafka.properties
- volumes
- - . maps to /code
- ports
- - 2181 zookeeper
- - 

# Running Kafka iteractively
## Start zookeeper
zookeeper-server-start /

Interacting after starting zookeeper and kafka
### kafka related cli
`kafka-topics --zookeeper 127.0.0.1:2181 --topic first_topic --create --partitions 3 --replication-factor 1`

Note the replication-factor has to be 1 for now because there's only one broker

List topics
`kafka-topics --zookeeper 127.0.0.1:2181 --list`

Describe topics
`kafka-topics --zookeeper 127.0.0.1:2181 --topic first_topic --describe`

Delete topics
`kafak-topics --zookeeper 127.0.0.1:2181 --topic second_topic --delete`

# Producers - produces messages
`kafka-console-producer --broker-list kafka:9092 --topic first_topic`
with acks
`kafka-console-producer --broker-list kafka:9092 --topic first_topic --producer-property acks=all`

Note -- kafka would create new topic with default configurations if produces messages to topic yet created

# Consumers - 
`kafka-console-consumer --bootstrap-server kafka:9092 --topic first_topic`
`kafka-console-consumer --bootstrap-server kafka:9092 --topic first_topic --from-beginning`
`kafka-console-consumer --bootstrap-server kafka:9092 --topic first_topic --group my-first-application`

the messages are sent to the consumers in the group
The offsets are commited by consumer group and only new messages since committed offsets will be read in by consumer (even if from-beginning option is given)

## Consumers groups
`kafka-consumer-groups --bootstrap-server kafka:9092 --list`
`kafka-consumer-groups --bootstrap-server kafka:9092 --describe --group my-second-application`
LAG means number of messages behind

## reset offsets
`kafka-consumer-groups --bootstrap-server kafka:9092 --group my-second-application --reset-offsets --to-earliest --execute --topic first_topic`