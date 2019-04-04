# Running docker-compose
`docker-compose up` to start kafka container
`docker-compose run kafka /bin/bash` to run kafka container service iteractively

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

