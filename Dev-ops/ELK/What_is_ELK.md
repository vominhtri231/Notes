# ELK

ELK is a log analysis platform, it includes:

- Elasticsearch: stores and indexes logs
- Logtash: collects logs and event data; parses, transforms data and sends them to Elasticsearch
- Kibana: a visualization tool that run ontop Elasticsearch

We can also include beats - single purpose data shipper to shipping data to logtash or directly to Elasticsearch.  
There multipe type of beats, such as filebeat, auditbeat, packagebeat, etc.  
They are more lightweight and can work as a log queue for reducing pressure for logtash with back-pressure sensitive protocol.
