# CCloud_Connect
Quicky get access to Confluent Cloud with this script. This repo runs a standalone Kafka connector which is preconfigured to connect to Confluent Cloud instance. This repo also includes the Confluent syslog source connector https://www.confluent.io/hub/confluentinc/kafka-connect-syslog, you can forward syslog to this instance and it will produce in Confluent Cloud.

To get started see below:

1. git clone repo
2. edit the .env file and fill in your credentials. To get the details Login to Confluent Cloud/Go to your Environment and follow steps below:
    *CLOUD_URL: cluster->Settings->Bootstrap server
    *CLOUD_TOKEN: cluster->API keys
    *CLOUD_SECRET: cluster->API keys
    *SCHEMA_REGISTRY_URL: Environment->Schema Registry->API endpoint
    *SCHEMA_REGISTRY_BASIC_AUTH: Environment->Schema Registry->API credentials (e.g. SCHEMA_REGISTRY_BASIC_AUTH='key':'secret')
3. Create your topic in Confluent Cloud e.g. KAFKA_TOPIC_NAME=?
4. docker-compose up -d


Once the instance is started, the Syslog connector is listening on localhot port 5555. You can test syslog by running the following, and you should see the message in Confluent Cloud console:
echo "<133>${0##*/}[$$]: Test syslog message from Netcat" | nc -w1 localhost 5555 