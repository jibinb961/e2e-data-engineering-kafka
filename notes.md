## Kafka

- Kafka is a cluster of brokers or servers that handles or stores the data which then can be consumed by consumer applications.

## Zookeeper

- Since Kafka takes in input from different data sources and then gives to different consumers, its important to have a system that can synchronize the operation. Zookeeper is basicallt a resource manager.
- Also we need to spin up an amazon instance.

## AMI 2023 ec2

- To install open jdk the usual sudo yum command wont work, itstead owe havve to install java using amazon corretto,
Install Amazon Corretto 8 as JRE. :  sudo yum install java-1.8.0-amazon-corretto
Install Amazon Corretto 8 as JDK. :  sudo yum install java-1.8.0-amazon-corretto-devel


## Setting up kafka broker and zookeper

Running the startup scripts for both will start both servers, but inorder to create atopic we need to set the inbound rules in the Amzon ec2 instance to allow any ipv4 traffic from all Ips. 

Also, to install jupyter i follwoed the below steps:

I am using python virtual env, or pyenv to use python in my mac. 

pip install notebook
pip install --upgrade pip
pip install jupyter

and finally tuype in 
jupyter notebook

which will startup a new server on port 8080 in your default web brwoser. 

The instances that we have are not big enough to continouly stream data. WE need more computing power. 

## To setup the services:

- Go to command_kafka.txt and follow the steps.

public ip  :  3.15.6.210
ssh -i "kafka-aws-ssd-type.pem" ec2-user@ec2-3-15-6-210.us-east-2.compute.amazonaws.com


## Setting up Amazon s3 :
- create an s3 bucket
- create a user under IAM service, and give them adimistrativeACces policy and create a key and ID.
- download amazon cli toosl using `brew install awscli`
- get the secret ID and key from s3 and configure it in AWS CLI using `aws configure`
- now python noteboook for consumer and producer.