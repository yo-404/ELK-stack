# ELK stack Architecture

![architecture-elk](https://www.elastic.co/guide/en/cloud/current/images/ec-logstash-beats-dataflow.png)

- Beats are essentially lightweight, purpose-built agents that acquire data and then feed it to Elasticsearch
    - Filebeat is designed to read files from your system, Metricbeat is used to collect metrics from servers and systems,
    - Packelbeat, a lightweight network packet analyzer, monitors network protocols
    - Winlogbeat is a tool specifically designed for providing live streams of Windows event logs
    -  Auditbeat is for Linux platforms to monitoring user and process activity, Heartbeat is a lightweight shipper for uptime monitoring 
- Logstash is an open source data collection engine with real-time pipelining capabilities. Logstash collects data from various input sources, executes different transformations and enhancements and then ships the data to vanious supported output destinations. 

- Elasticsearch cluster is not limited to a single machine , because of it you can easily scale your system horizontally to handle higher traffic and larger data sets


## Elasticsearch Component overview

Cluster: A cluster ia s collection of nodes which together golds data and provides joined indexing and search capabilities

Node: A node is an elasticsearch instance

Index:  An index is a collection of documents which has similar characteristics. e.g., customer data, product catalog. It is very useful while performing indexing, search, update, and delete operations. It allows you to define as many indexes in one single cluster. 

Document:  It is the basic unit of information which can be indexed. It is expressed in JSON (key: value) pair. Every single Document is associated with a type and a unique id. 

Shard:  Shards are individual instances of a Lucene index. Every index can be split into several shards to be able to distribute data. Each index is comprised of shards across one or many nodes. There are primary and replica shards