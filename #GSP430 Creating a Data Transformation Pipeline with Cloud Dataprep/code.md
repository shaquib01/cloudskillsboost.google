# GSP430 Creating a Data Transformation Pipeline with Cloud Dataprep
## Run in cloudshell
```cmd
bq mk ecommerce
bq query --use_legacy_sql=false \
'#standardSQL
 CREATE OR REPLACE TABLE ecommerce.all_sessions_raw_dataprep
 OPTIONS(
   description="Raw data from analyst team to ingest into Cloud Dataprep"
 ) AS
 SELECT * FROM `data-to-insights.ecommerce.all_sessions_raw`
 WHERE date = "20170801";'
wget https://github.com/shaquib01/cloudskillsboost.google/raw/master/%23GSP430%20Creating%20a%20Data%20Transformation%20Pipeline%20with%20Cloud%20Dataprep/flow_Ecommerce_Analytics_Pipeline.zip download flow_Ecommerce_Analytics_Pipeline.zip
```
____
### Dataprep > Accept all conditions > flow > import flow > select the file 
### Remove first file from flow > Click + > import dataset > Bigquery > ecommerce > click + > import & add to flow > select
### Output > Run > Edit > Bigquery > GCP id > ecommerce > create new table > update > Run
____
