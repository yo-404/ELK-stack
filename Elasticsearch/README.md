# Elasticsearch

Elasticsearch is a distributed, free and open search and analytics engine for all types of data, including textual, numerical, geospatial, structured, and unstructured. Elasticsearch is built on Apache Lucene and was first released in 2010 by Elasticsearch N.V. (now known as Elastic). Known for its simple REST APIs, distributed nature, speed, and scalability, Elasticsearch is the central component of the Elastic Stack, a set of free and open tools for data ingestion, enrichment, storage, analysis, and visualization. Commonly referred to as the ELK Stack (after Elasticsearch, Logstash, and Kibana), the Elastic Stack now includes a rich collection of lightweight shipping agents known as Beats for sending data to Elasticsearch. 

# What is Elasticsearch used for?

The speed and scalability of Elasticsearch and its ability to index many types of content mean that it can be used for a number of use cases:

- Application search
- Website search
- Enterprise search
- Logging and log analytics
- Infrastructure metrics and container monitoring
- Application performance monitoring
- Geospatial data analysis and visualization
- Security analytics
- Business analytics

# Installation

#### on ubuntu

```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
sudo apt-get install apt-transport-https

echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list

sudo apt-get update && sudo apt-get install elasticsearch


sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable elasticsearch.service

sudo systemctl start elasticsearch.service

```
#### to confirm the installation

`curl 127.0.0.1:9200`

### using docker

```
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.12.1

docker run --name elasticsearch -d -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.12.1

docker logs elasticsearch -f

docker exec -it elasticsearch bash

curl http://localhost:9200


curl -X PUT http://localhost:9200/newindex

curl -X GET http://localhost:9200/newindex

curl -X GET http://localhost:9200/newindex?pretty

```

# What is Elasticsearch Index

An index is like a 'database' in a relational database

- MYSQL → Databases → Tables → Columns and rows
- Elasticsearch → Indices → Types → Documents with Properties

## Creating Indexes

#### Index Rules

- The index name must be lower case only.
- The index names cannot start with a dash (-), an underscore (_), or an addition sign (+)
-  The names cannot be . or ..
-  Index names cannot include special characterssuch as: \, /, *, 2, “, <, >, |, (space character), ,, # 
- The length of index names must be less than 255 bytes.
- The names that start with a . are reserved for hidden indices and internal indices used by Elasticsearch plugins. 

#### Creating Index

`curl -XPUT "localhost:9200/test_indext?pretty?"`

-XPUT - used to create indexes /override
-POST - writing info into the index
-GET - Getting info from the index

#### Accessing Index

`curl -X GET "localhost:9200/test_indext?pretty?"`

#### To delete Index 

`curl -XDELETE "localhost:9200/test_indext?pretty?"`

## Components of index body

- Index body:
    - Aliases : specifices alias name for the index you want to create
    - Settings : This defines the configuration option for the index . If you fail to specify any parameter , the index gets created using default configurations
    - Mappings : This defines the mapping for fields in the index. 
                 The specifications you can include in mappings include: 
                  - The field name 
                  - The data type 
                  - The mapping parameter 


### Example 

```yaml
PUT /test_index1?pretty
{
    "settings" : {
        "number_of_shards" : 2,
        "number_of_replicas" : 1
    },
    "mappings" : {
        "properties" : {
            "tags" : { "type" : "keyword" },
            "updated_at" : { "type" : "date" }
        }
    }
}
```
`curl -XPUT "localhost:9200/test_indext?pretty?" -H 'Content-Type:applicatiom/json '-d' <json index content>`

### Putting content into indexes

##### example 

```
curl -XPUT "localhost:9200/product?pretty?" -H 'Content-Type:applicatiom/json '-d'
{
    "name": "OnePlus",
    "camera": "64MP",
    "storage": "256GB",
    "display": "6.4inch",
    "battery": "5,000mAh",
    "reviews": ["Good"]
   
}
```

## Query on indexes

`curl -H 'Content-type: application/json' -XGET "localhost:9200/product/_search?pretty?" -d `

## importing values from other json files in bulk

`curl -H 'Content-type: application/json' -XPUT "localhost:9200/newindexname/_bulk?pretty?" --data-binary @filename `

example -

`curl -H 'Content-type: application/json' -XPUT "localhost:9200/shakespeare/_bulk?pretty?" --data-binary shakespeare_6.0.json `

#### searching query from index

```
`curl -H 'Content-type: application/json' -XGET "localhost:9200/shakespeare/_search?pretty?" -d `
{
    "query": {
        "match_phrase": {
            "text_entry" : "So shaken as we are"
        }
    }
}
```

