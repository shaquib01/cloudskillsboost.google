# Create a Cosmetic Anomaly Detection Model using Visual Inspection AI
```
gcloud services enable visualinspection.googleapis.com
export PROJECT_ID=$(gcloud config get-value core/project)
gsutil mb gs://${PROJECT_ID}
gsutil -m cp gs://cloud-training/gsp897/cosmetic-test-data/*.png \
gs://${PROJECT_ID}/cosmetic-test-data/
gsutil ls gs://${PROJECT_ID}/cosmetic-test-data/*.png > /tmp/demo_cosmetic_images.csv
gsutil cp /tmp/demo_cosmetic_images.csv gs://${PROJECT_ID}/demo_cosmetic_images.csv

echo "VISUAL INSPECTION AI LINK : https://console.cloud.google.com/ai/visual-inspection/datasets/create?project=$PROJECT_ID"
```
#--CLICK VISUAL INSPECTION AI LINK > 
>DATASET NAME : ````cosmetic ````
>Objective : ````Cosmetic Inspection```` 
>Annotation : ````Polygon````
>Region : ````US Central1````

>ONCE DATASET IS CREATED > CLICK BROWSE > SELECT <YOUR_PROJECT_ID> > SELECT demo_cosmetic_images.csv > CLICK ````CONTINUE ````
