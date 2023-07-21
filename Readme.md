```
docker-compose -f docker-compose-kafka.yaml up --build -d

docker-compose -f docker-compose-cluster.yaml up --build -d

docker exec -it <CONTAINER ID> bash


//Topic

 - Create Topic
kafka-topics.sh --create --topic <TOPIC_NAME> --bootstrap-server localhost:9092
kafka-topics.sh --create --topic <TOPIC_NAME> --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1

 - Get Topic Info
kafka-topics.sh --list --bootstrap-server localhost:9092
kafka-topics.sh --describe --bootstrap-server localhost:9092 --topic <TOPIC_NAME> 

 - Delete Topic
kafka-topics.sh --delete --topic <TOPIC_NAME> --bootstrap-server localhost:9092


//Producer
kafka-console-producer.sh --topic <TOPIC_NAME> --bootstrap-server localhost:9092
kafka-console-producer.sh --topic <TOPIC_NAME> --bootstrap-server localhost:9092 --producer-property acks=all  
###
- acks=0 producer จะ produce แล้วไม่รอผลตอบของ broker ว่าได้รับข้อมูลหรือยัง
- acks=1 producer จะ produce และรอผลตอบจาก leader partition ว่าได้รับข้อมูลหรือยัง
- acks=all producer จะ produce และรอผลจนข้อมูลถูกบันทึกเข้า replica แล้ว
###

//Consumer
kafka-console-consumer.sh --topic <TOPIC_NAME> --bootstrap-server localhost:9092
kafka-console-consumer.sh --topic <TOPIC_NAME> --bootstrap-server localhost:9092 --from-beginning   #Read from start from partition not in consumer
kafka-console-consumer.sh --topic <TOPIC_NAME> --bootstrap-server localhost:9092 --group <GROUP_NAME>
###
--partition <partition_id>
###
kafka-console-consumer.sh --topic frankly --bootstrap-server localhost:9092 --partition 0

//Consumer Group

 - Get Consumer Group Info
kafka-consumer-groups.sh --bootstrap-server localhost:9092 --list
kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe --group <GROUP_NAME>

 - Reset Offsets
kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group <CONSUMER_GROUP> --reset-offsets --to-earliest --execute --topic <TOPIC_NAME>
kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group <CONSUMER_GROUP> --reset-offsets --to-earliest --execute --all-topics

 - Delete Consumer Group
kafka-consumer-groups.sh --bootstrap-server localhost:9092 --delete --group <CONSUMER_GROUP>

//KRAFT
kafka-metadata-quorum.sh --bootstrap-server localhost:9092 describe --status
kafka-dump-log.sh --cluster-metadata-decoder --files <PATH_TO_LOG>

```
//link
https://github.com/bitnami/containers/blob/main/bitnami/kafka/README.md
