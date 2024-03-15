# Bash script to create dataset in BigQuery
# Authenticate and set project
gcloud auth login
gcloud config set project qwiklabs-gcp

# Create dataset
bq mk --location=US --dataset imported_billing_data

# Bash script to import data into BigQuery table
# Authenticate and set project
gcloud auth login
gcloud config set project qwiklabs-gcp

# Import data into table
bq load --autodetect --skip_leading_rows=1 imported_billing_data.sampleinfotable gs://cloud-training/archinfra/export-billing-example.csv
