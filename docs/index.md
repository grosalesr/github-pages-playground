# Landing page

Elastic rapid course can be found [here](technical_guide.md)

Elastic deployment guide can be found here

|Hostname|CPU|RAM|App Deployed|Role|
| --- | --- | --- | --- | --- |
| elastic1 | 4 | 32 GB | Elasticsearch | master node |
| elastic4 | 4 | 32 GB | * Elasticsearch | coordinating node |
|          |   |       | * Kibana | NA |
| elastic5 | 2 | 4 GB | Logstash | NA |
