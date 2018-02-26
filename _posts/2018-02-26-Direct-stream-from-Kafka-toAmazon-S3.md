---
layout: post
comments: true
title: Setting up direct stream from Kafka to Amazon S3 bucket using Kafka Connect.
---


<p align="justify">
Hello! Here we will learn how to set up a Kafka Connector that will put messages from Kafka to S3 bucket on Amazon.
</p>

First things first:

1. Create a bucket on Amazon and add a policy.
On the S3 console page got o: YourBucket -> Permissions tab -> Bucket Policy button.

```

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "statement1",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::userID:user/username"
            },
            "Action": [
                "s3:GetBucketLocation",
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::bucketName"
        },
        {
            "Sid": "statement2",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::userID:user/username"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::bucketName/*"
        }
    ]
}
```

2. Create an AWS user and add user's inline policy.
On the IAM console go to : Users -> youUser ->  Permissions tab -> Add inline policy button

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PermissionForObjectOperations",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject"
            ],
            "Resource": [
                "arn:aws:s3:::bucketName/*"
            ]
        }
    ]
}
```
3. Set up a machine with Kafka Connect software. Let's assume you wok on Centos (I do). You will need:
* <a href="http://ftp.man.poznan.pl/apache/kafka/0.11.0.2/kafka_2.11-0.11.0.2.tgz">Kafka software</a> 
* A java package (java-1.8.0-openjdk.x86_64)
* <a href="https://www.confluent.io/download/">A Confluent package</a>
* A user (I named mine ***kafka-connect***)

Once you have downloaded/installed all the packages, put them in the kafka-connect home directory. Next, you have to modify 
***connect_distributed.properties*** file (should be under /home/kafka-connect/kafka/kafka_2.11-0.11.0.2/config/connect-distributed.properties):

```
bootstrap.servers=serverIP:9092
group.id=super-unique-group-name-something-like-ghTV678
key.converter.schemas.enable=false
value.converter.schemas.enable=false
internal.key.converter=org.apache.kafka.connect.json.JsonConverter
internal.value.converter=org.apache.kafka.connect.json.JsonConverter
internal.key.converter.schemas.enable=false
internal.value.converter.schemas.enable=false
offset.storage.topic=super-unique-group-name-something-like-ghTV678
offset.storage.replication.factor=3
config.storage.topic=super-unique-group-name-something-like-ghTV678
config.storage.replication.factor=3
status.storage.topic=super-unique-group-name-something-like-ghTV678
status.storage.replication.factor=3
offset.flush.interval.ms=60000
plugin.path=/home/kafka-connect/opt/confluent-4.0.0/share/java
```

Now you may run your instance of Kafka:
`/home/kafka-connect/kafka/kafka_2.11-0.11.0.2/bin/connect-distributed.sh /home/kafka-connect/kafka/kafka_2.11-0.11.0.2/config/connect-distributed.properties`

Once Kafka instance is launched, you need to create the CONNECTOR, which will catch the messages and send them to S3 bucket.

```
curl -s -X POST -H "Content-Type: application/json" --data '
{
"name": "Connector Name",
"config": {
"connector.class": "io.confluent.connect.s3.S3SinkConnector",
"tasks.max": "3",
"topics": "topics you would like to catch",
"s3.region": "your S3 region (#captainObvious)",
"s3.bucket.name": "BucketName",
"s3.part.size": "5242880",
  "flush.size": "how many messages in file",
"storage.class": "io.confluent.connect.s3.storage.S3Storage",
"format.class": "io.confluent.connect.s3.format.json.JsonFormat",
 "schema.generator.class": "io.confluent.connect.storage.hive.schema.DefaultSchemaGenerator",
"partitioner.class": "io.confluent.connect.storage.partitioner.DefaultPartitioner",
"schema.compatibility": "NONE",
"name": "Connector Name"
}
 }' http://127.0.0.1:8083/connectors
 ```
<p align="justify">
There. It was not so complicated, wasn't it? Actually, it took us some time to define the final config, but we never touched KafkaConnect or S3 before, so..... much googling ;)</p>
