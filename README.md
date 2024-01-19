
# Log-Ingestion-OpenSearch

Log ingestion is a way to transform the unstructured log data into structured log data and ingest into Opensearch.

Here we injest fake apache logs using a fake apache log generator from https://github.com/graytaylor0/Fake-Apache-Log-Generator


## Tools

#### FluentBit	
It is used as log collector that collects log data from the application and sends it to Data Prepper
#### Data Prepper	
It transforms the unstructured log data data into a structured format and sends to Opensearch cluster
#### Opensearch	
It is place where the structured log data is indexed for futher search and analytics activities
#### Opensearch Dashboard	
It helps in search and analytics of the indexed data and for data visualization


## Installation

Start open search node
```bash
git clone https://github.com/Shades-en/Log-Ingestion-OpenSearch.git
cd Log-Ingestion-OpenSearch
docker-compose --project-name log-ingestion up
```

Start Data prepper
```bash
cd dataprepper
docker-compose --project-name log-ingestion up
```

Start Fluent-bit
```bash
cd fluentbit
docker-compose --project-name log-ingestion up
```





    
## Usage/Examples

Run Fake apache log generator
```bash
cd fluentbit
python3 apache-fake-log-gen.py -n 0 -s 2 -l "CLF" -o "LOG" -f "test.log"
```

You should start seeing records flowing into fluent-bit


Go to Opensearch Dashboard at http://localhost:5601

### Create Index
You will need to create an index pattern for the index provided in your pipeline.yaml in order to see them. 

You can do this by going to Stack Management -> Index Pattterns. Now start typing in the name of the index you sent logs to (in this guide it was nginx_logs), and you should see that the index pattern matches 1 source. 

Click Create Index Pattern, and you should then be able to go back to the Discover tab to see your processed logs.
