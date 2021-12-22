# Landing page

Elastic rapid course can be found [here](technical_guide.md)

Elastic deployment guide can be found here

|Hostname|CPU|RAM|App Deployed|Elasticsearch Node Role|
| --- | --- | --- | --- | --- |
| elastic1 | 4 | 32 GB | Elasticsearch | master node |
| elastic4 | 4 | 32 GB | * Elasticsearch \n * Kibana | coordinating node |
| elastic4 | 4 | 32 GB | <ul><li>Elasticsearch</li><li>Kibana</li></ul> | coordinating node |
| elastic4 | 4 | 32 GB | Elasticsearch<br>Kibana | coordinating node<br>NA |
| elastic5 | 2 | 4 GB | Logstash | NA |
