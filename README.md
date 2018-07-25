# docker-elk
ELK stack for spring-boot/java applications using logback.
Contents:
1. docker-compose.yml
2. logstash_config
      |--------------> logstash.conf

version: '2.1'

services:

  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:6.3.2
    container_name: elasticsearch
    environment:
       - cluster.name=docker-cluster
       - bootstrap.memory_lock=true
       - xpack.security.enabled=false
       - discovery.type=single-node
       - discovery.zen.minimum_master_nodes=1
       - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    mem_limit: 2g
    ports:
      - "9200:9200"
      - "9300:9300"

  logstash:
    image: docker.elastic.co/logstash/logstash:6.3.2
    container_name: logstash
    command: logstash -f /etc/logstash/conf.d/logstash.conf
    volumes:
     - ./logstash_config:/etc/logstash/conf.d
    ports:
     - "5044:5044"
    links:
     - elasticsearch

  kibana:
    image: docker.elastic.co/kibana/kibana:6.3.2
    container_name: kibana
    environment:
     - ELASTICSEARCH_URL=http://elasticsearch:9200
    ports:
     - "5601:5601"
    links:
     - elasticsearch

volumes:
  esdata1:
      driver: local
