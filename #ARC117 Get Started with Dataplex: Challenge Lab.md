# Get Started with Dataplex: Challenge Lab
```
gcloud services enable \
  dataplex.googleapis.com \
  datacatalog.googleapis.com
export PROJECT_ID=$(gcloud config get-value project)
gcloud config set compute/region $REGION

gsutil mb -c standard -l $REGION gs://$PROJECT_ID

gcloud dataplex lakes create customer-engagements \
   --location=$REGION \
   --display-name="Customer Engagements" \
   --description="Customer Engagements Domain"

gcloud dataplex zones create raw-event-data \
    --location=$REGION \
    --lake=customer-engagements \
    --display-name="Raw Event Data" \
    --resource-location-type=SINGLE_REGION \
    --type=RAW \
    --discovery-enabled \
    --discovery-schedule="0 * * * *"

gcloud dataplex assets create raw-event-files \
--location=$REGION \
--lake=customer-engagements \
--zone=raw-event-data \
--display-name="Raw Event Files" \
--resource-type=STORAGE_BUCKET \
--resource-name=projects/$PROJECT_ID/buckets/$PROJECT_ID \
--discovery-enabled 

echo "REGION : $REGION"
echo "DATAPLEX TAG TEMPLATE : https://console.cloud.google.com/dataplex/templates/create?project=$PROJECT_ID"
```
##  OPEN DATAPLEX TAG TEMPLATE LINK FROM TERMINAL TO DO CONSOLE STEPS 

### TASK 3
>OPEN TAG TEMPLATE >CREATE TAG TEMPLATE
##### TEMPLATE DISPlAY NAME : Protected Raw Data Template

#### TEMPLATE ID : LEAVE AS IT IS

#### LOCATION : REGION GIVEN IN LAB

##### CLICK ADD FIELD :-

>FIELD DISPLAY NAME :
```
Protected Raw Data Flag
```
>FIELD ID : LEAVE AS IT IS

>TYPE : Enumerated

>VALUE 1 : Y

>VALUE 2 : N

>CLICK CREATE

## TASK 3
>CLICK SEARCH FROM LEFT SIDE MENU

>Search
```
Raw Event Data
```
>CLICK
>CLICK ATTACH TAGS BUTTON

>SELECT THE FOLLOWING FROM DROPDOWN :

###### 1.
>SELECT Protected Raw Data Template

###### 2.

>SELECT Y

>CLICK SAVE
