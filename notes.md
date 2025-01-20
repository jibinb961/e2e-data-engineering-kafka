# Kafka and Zookeeper with AWS Setup

## Kafka
Kafka is a distributed event streaming platform capable of handling trillions of events a day. At its core, Kafka is a cluster of brokers or servers that handle or store data, which can then be consumed by various consumer applications. Here are the key components and concepts:

### Key Concepts:
- **Producers**: Applications that publish data to Kafka topics.
- **Topics**: Categories or feed names to which records are sent by producers. Each topic is partitioned for scalability.
- **Brokers**: Kafka servers that store and serve data. A Kafka cluster consists of multiple brokers.
- **Consumers**: Applications that subscribe to topics and process the data.
- **Partitions**: Topics are divided into partitions, allowing parallel processing and fault tolerance.

### Features:
- **Scalability**: Kafka is designed to handle large-scale data streams across multiple brokers.
- **Durability**: Kafka replicates partitions across brokers, ensuring data durability.
- **Real-time**: Supports low-latency data streaming.

## Zookeeper
Zookeeper is a centralized service for maintaining configuration information, naming, synchronization, and providing group services. It is often used alongside Kafka to manage cluster metadata and operations.

### Key Responsibilities:
1. **Cluster Management**: Tracks the status of Kafka brokers and keeps track of the Kafka cluster's metadata.
2. **Leader Election**: Ensures that one broker is elected as the leader for each partition.
3. **Synchronization**: Provides a consistent state across the Kafka cluster by ensuring synchronization of operations.
4. **Configuration Management**: Maintains configuration information for the Kafka cluster.

### Zookeeper and Kafka Together:
- **Metadata Management**: Zookeeper manages the metadata for Kafka topics, partitions, and replicas.
- **Fault Tolerance**: Zookeeper monitors the status of Kafka brokers and triggers failover when a broker goes down.
- **Coordination**: Zookeeper ensures that all brokers, producers, and consumers work together in a coordinated manner.

## Installing Kafka and Zookeeper on Amazon EC2
### Prerequisites:
1. **Spin up an Amazon EC2 Instance**:
   - Choose an Amazon Machine Image (AMI) 2023.
   - Ensure that the instance has sufficient compute power for streaming tasks.

2. **Install OpenJDK**:
   - Use Amazon Corretto to install Java (required for Kafka):
     ```bash
     sudo amazon-linux-extras install corretto8
     ```
   - Alternate commands for specific JRE or JDK installations:
     ```bash
     sudo yum install java-1.8.0-amazon-corretto      # Install JRE
     sudo yum install java-1.8.0-amazon-corretto-devel # Install JDK
     ```

### Setting Up Kafka Broker and Zookeeper
1. **Download Kafka**:
   - Navigate to the Kafka download page and fetch the latest Kafka tarball.
   - Extract the downloaded file and move it to a desired directory.

2. **Configure Kafka and Zookeeper**:
   - Edit `server.properties` for Kafka configuration.
   - Edit `zookeeper.properties` to configure Zookeeper.

3. **Start Services**:
   - Start Zookeeper:
     ```bash
     bin/zookeeper-server-start.sh config/zookeeper.properties
     ```
   - Start Kafka Broker:
     ```bash
     bin/kafka-server-start.sh config/server.properties
     ```

4. **Set Inbound Rules**:
   - Update EC2 instance security group rules to allow inbound traffic from any IPv4 address on required ports (e.g., 9092 for Kafka).

5. **Create Topics**:
   - Use Kafka commands to create topics:
     ```bash
     bin/kafka-topics.sh --create --topic <topic-name> --bootstrap-server <broker-address>
     ```

### Jupyter Notebook Installation
If you are using a Python virtual environment (e.g., pyenv), follow these steps:
```bash
pip install notebook
pip install --upgrade pip
pip install jupyter
jupyter notebook
```
- The server starts on port 8080 and opens in the default web browser.

### Note:
Ensure the EC2 instance has sufficient compute power for streaming tasks, as underpowered instances may not handle continuous data streams effectively.

## Setting Up Amazon S3
1. **Create an S3 Bucket**:
   - Go to the S3 service and create a new bucket for storing Kafka data.

2. **Set Up IAM User**:
   - Create an IAM user with the `AdministratorAccess` policy.
   - Generate an access key and secret key for the user.

3. **Install AWS CLI**:
   - Install AWS CLI tools:
     ```bash
     brew install awscli
     ```
   - Configure AWS CLI with the access key and secret key:
     ```bash
     aws configure
     ```

4. **Kafka Consumer and Producer**:
   - Set up Kafka producers and consumers to send data to the S3 bucket.

5. **Amazon Glue and Athena**:
   - **Glue**:
     - Create a crawler in Amazon Glue to process data from the S3 bucket.
     - Run the crawler to generate a table for the JSON data in S3.
     - Assign an IAM role with `AdministratorAccess` to the Glue service.
   - **Athena**:
     - Use Athena to query the data table created by Glue.
     - Specify a target location in S3 to save query results.

6. **Result**:
   - Use Athena queries to analyze the processed data and extract insights.

## To Set Up the Services
- Refer to `command_kafka.txt` for specific commands and configurations.
