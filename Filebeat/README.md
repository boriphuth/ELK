# Download
Filebeat can be installed as a service otherwise you have to download the zip folder to extract (this solution could be useful to discover the tool or if you only have windows installed on your machine but not for a stable solution).  
For the rest of this document, we use version 7.3 of filebeat, which can be downloaded at https://www.elastic.co/downloads/past-releases/filebeat-7-3-0  
Choose the version that corresponds to your operating system.
## The key folders  <_linux_OS_>
There is 3 interestion paths to know:
- **/var/log/filebeat:** In this folder you can find logs generated by filebeat. This folder is useful for a debugging need
- /var/lib/filebeat: Filebeat stores data in relation to messages sent to your receiver
- /etc/filebeat : In this folder, you can find the configuration file "filebeat.yml"
# Architecture

![Screenshot](kafka-min.png)

# Explanation

**Filebeat:** is an agent to ship data. If it's configured well, you can deal with a lot of data without any risk of data loss. It is possible to send data to logstash, elasticsearch,kafka...However, **you can use a single output**.

**Kafka:**  is like a queue that we can use to store data per topic. Topic is similar to a key that is used to store a type of data. For example, if you have two server that generate log files, you can create two topics (server1-log, server2-log) and set-up filebeat to send log from server1 to the first topic and from server2 to the other one. The possibility to have multiple topics could be usefull to deal with the constraint to have only one output in filebeat.

**Logastash:** I recommend to use logstash and not another software to parse data ingested into kafka, beacause it's easier to set-up the output and sending data to Elasticsearch. 

**Elasticsearch:** Elasticsearch is a distributed, RESTful search and analytics engine capable of addressing a growing number of use cases.

**Kibana:** is an open source data visualization plugin for Elasticsearch.