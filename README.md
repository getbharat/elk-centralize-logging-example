# elk-centralize-logging-example
Centralize logging in microservice architecture using ELK.

Download ELK binary distrubution. Run the project and follow below steps sequently. Hit the rest endpoint to generate logs messages. 

1 - To start [Elasticsearch](https://www.elastic.co/downloads/elasticsearch), go to bin folder of the installation directory and execute below command. Once the engine is started, it can be accessed on default port 9200.
          
     elasticsearch.bat 

2- To access [Kibana](https://www.elastic.co/downloads/kibana), edit kibana.yml file to uncomment 'elasticsearch.hosts', it should point elasticsearch. Now go to the bin folder and excute the below command. Access kibana at default port 5601.

     kibana.bat 
     
3- To run [Logstash](https://www.elastic.co/downloads/logstash), you need logstash.conf file that need to be placed in logstash's bin folder. An example config is given below.
   ```
  input {
  file {
    # The path of log file
    path => "C:\logs\elk-stack.log"
	  start_position => "beginning"
  }
}


output {
  stdout { 
  codec => rubydebug 
  }
  # send logs to elasticsearch
  elasticsearch { 
  hosts => ["localhost:9200"] 
  }
}
```
After adding the file, go to bin and run 'logstash -f logstash.conf'. Logstash can be accessed at its default port 9600.
