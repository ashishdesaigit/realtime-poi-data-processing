# realtime-poi-data-processing
POI data streaming and processing in real time

POI Producer 
- Spring app 
- MQTT / Websocket / HTTP 
- Kafka client 
- containeriszed 
- k8s / AWS / GCP / Azure / Any Cloud



Stream Processor 
- Kafka cluster 
- Deployed on k8s / AWS / GCP / Any Cloud


POI consumer
- Spring app with apache streams 
- containerized 
- configured with kafka cluster 
- given some app name 
- configured with consumer group id 
- metric endpoints configured 
- logstash configured 
- ready for deployment on k8s / AWS / GCP / Any Cloud



Data Sink 
- Apache kafka connector 
- From topic to Cassandra cluster data transfer 


POI Reporting Dashboard - 
ELK 

System Monitoring Dashboard -
Micrometer + prometheus + grafana / newrelic / datadog 


POI Store 
- cassandra cluster 
