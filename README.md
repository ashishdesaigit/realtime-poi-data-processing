# realtime-poi-data-processing
POI data streaming and processing in real time.

Here is the overall solution approach:

![Alt text](./overview.svg)
<img src="./doc/overview.svg">

### User cases Considered :

- PoI Data collection activity might scale up or scale down. 

- Errors can occur, validation Rules might change in flight. 
For all such reasons we need `replay` functionality.

- PoI record fields might change at the producer's end ,
So serialiser and deserialiser should have forward and backward compatibilities.

- Use case of `exactly once processing` is considered. It might be expensive in distributed environment 

### Assumptions :
- Structure of record exchanged might change 
- Processed PoI data gets saved in Database layer in the same format. ( Same schema )

### Constraints :
- Database selection for  'Processed Data Sink' component. This is an informed decision.
Since we are using kafka data connectors - we need to choose from supported databased.
List can be found here ( https://www.confluent.io/hub/kafka-connectors-3 )


### List Components
1. POI Producer 
2. Stream Processor
3. POI consumer
4. Data Sink
5. POI Store
6. POI Reporting Dashboard
7. System Monitoring Dashboard

### Tech stack for each Components
 POI Producer 
- Java 
- Spring Boot 
- MQTT / Websocket / HTTP 
- Apache Streams API to produce on `poi-unprocessed-topic` 
- Serializer Format : protobuf / Json  
- Containerised application
- metrics endpoints configured 
- logstash configured 
- Deployed on k8s / AWS / GCP / Azure / Any Cloud


Stream Processor 
- Kafka cluster (  `poi-unprocessed-topic` ,  `poi-processed-topic` )
- Configured for `exactly-once` semantics
- Deployed on k8s / AWS / GCP / Any Cloud


POI consumer
- Java
- Spring app 
- Apache Streams API  to consume `poi-unprocessed-topic` and produce on `poi-processed-topic`
- configured for kafka cluster ( app-name , consumer-group-id )
- Deserializer Format : protobuf / Json  
- metrics data endpoints configured 
- logstash configured 
- containerized 
- ready for deployment on k8s / AWS / GCP / Any Cloud



Data Sink 
- Apache kafka connector 
- Data transfer from `poi-processed-topic` to Cassandra cluster 


POI Reporting Dashboard - 
- ELK Stack

System Monitoring Dashboard -
- (Micrometer + prometheus + grafana) / newrelic / Datadog 


POI Store 
- Cassandra Cluster 
