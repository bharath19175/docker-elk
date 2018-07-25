# docker-elk
ELK stack for spring-boot/java applications using logback.

# Contents:
1. docker-compose.yml
2. logstash_config
      |--------------> logstash.conf

# Steps to run
1. clone the repository
      |--------------> git clone https://github.com/bharath19175/docker-elk.git
2. cd docker-elk
3. cd docker-elk-for-springboot-logback
4. docker-compose up -d

# Check if the containers are running 
1. docker ps

# check if elasticsearch and kibana are running on ports 9200 and 5601
1. open browser
2. enter "localhost:9200" for elasticsearch
3. enter "localhost:5601" for kibana
4. you should see output in localhost:9200 and kibana dashboard on localhost:5601

# That's it!!!!!!!
make neccesory changes in your spring-boot java application's logback.xml file.

# important!!!!!!!
In the appender block of logback.xml add destination as "localhost:5044".

# example
```
  <appender name="logstash" class="net.logstash.logback.appender.LogstashTcpSocketAppender>
      <destination>localhost:5044</destination>
      <encoder> </encoder>
  </appender>
```
