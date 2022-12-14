# kafkaTopicIncreaseReplicationFactor
Script to help with increasing Kafka topic Replication Factor

[Reference https://gist.github.com/uarun/da30d8ef52b5d57b145cd13694c8acdc]

# Increasing replication factor for a topic

1. Create a custom reassignment plan. Got to the last section to generate the file (My Script to generate the Json File)
2. Run Kafka partition reassignment script:

       kafka-reassign-partitions --zookeeper $ZOOKEEPER_CONNECT \
           --reassignment-json-file /home/liquidnt/inc-replication-factor.json  \
           --execute
   
3. Verify if the assignment was successful

       kafka-reassign-partitions --zookeeper $ZOOKEEPER_CONNECT \
           --reassignment-json-file /home/liquidnt/inc-replication-factor.json  \
           --verify
           
4. More verifications

        ./kafka-topics --zookeeper $ZOOKEEPER_CONNECT --describe --topic <topicname>
        

# My Script to generate the Json File
The most important part of this process is the json file that needs to be created. To make it automatable, I have written a small script that should be able to generate an output consisting of the json provided:  
```
topic= "name of the topic"  
partition= "total partitions in the topic"  
brokers= "number of brokers"  
replicationfactor= "desired replication factor"  
```
  
While using the script in bash you can do 
```source createKafkaRebalanceJson``` 
to load its member functions in memory and then you can call the function as follows:  
  
  
sample usage: (topic= test, partition=26, brokers=5, replicationfactor=3)  
```
getKafkaResizeJson "test" 26 5 3 >sample.json
```  
##### Note: The sample output for the above command is also provided as sample.json
