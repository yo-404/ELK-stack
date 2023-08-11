# Logstash

- Logstash is an open source datalcollection engine with real-time pipelining capabilities 
- Logstash can dynamically unify data from different sources and normalize the data into destinations of your chouce
- Horizontally scalable data processing pipeline with strong elasticsearch and kibana synergy
- Over 200 plugins available ,plus the flexibilty of creating and contributing your own

## How logstash works

- The logstash event processing pipeline has three stages :
 input → Filters → outputs

- Some of the more commonly used **inputs** are
    - file
    - syslog
    - redis
    - beats

- some of the commonly used **outputs** are
    - elasticsearch
    - file
    - graphite
    - statsd

# logstash architecture

![architecture-logstash](https://blogs.bmc.com/wp-content/uploads/2021/11/logstash.png)


# installation

#### using docker

```
docker pull docker.elastic.co/logstash/logstash:8.9.0

wget https://artifacts.elastic.co/cosign.pub 
cosign verify --key cosign.pub docker.elastic.co/logstash/logstash:8.9.0

```

#### creating a sample logstash config file

```
$mkdir /config-dir

$ cat logstash.conf
input {
stdin {}
}

output {
   elasticsearch { hosts => ["elasticsearch:9200"] }

}

```

```
docker run -h logstash --name logstash --link elasticsearch:elasticsearch -it --rm -v "$PWD":/config-dir logstash -f /config-dir/logstash.conf
curl http://localhost:9200/_cat/indices
```