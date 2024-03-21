## TASK 1
### CREATE OR REPLACE TABLE
  ```
taxirides.taxi_training_data_474 AS 
SELECT
  (tolls_amount + fare_amount) AS fare_amount_138,
  pickup_datetime,
  pickup_longitude AS pickuplon,
  pickup_latitude AS pickuplat,
  dropoff_longitude AS dropofflon,
  dropoff_latitude AS dropofflat,
  passenger_count AS passengers,
FROM
  taxirides.historical_taxi_rides_raw
WHERE
  RAND() < 0.001
  AND trip_distance > 4
  AND fare_amount >= 2.0
  AND pickup_longitude > -78
  AND pickup_longitude < -70
```

## TASK 2
### CREATE OR REPLACE MODEL 
```
taxirides.fare_model_551
TRANSFORM(
  * EXCEPT(pickup_datetime)

  , ST_Distance(ST_GeogPoint(pickuplon, pickuplat), ST_GeogPoint(dropofflon, dropofflat)) AS euclidean
  , CAST(EXTRACT(DAYOFWEEK FROM pickup_datetime) AS STRING) AS dayofweek
  , CAST(EXTRACT(HOUR FROM pickup_datetime) AS STRING) AS hourofday
)
OPTIONS(input_label_cols=['fare_amount_138'], model_type='linear_reg')
AS

SELECT * FROM taxirides.taxi_training_data_474

```
### TASK 3
```
CREATE OR REPLACE TABLE taxirides.2015_fare_amount_predictions
  AS
SELECT * FROM ML.PREDICT(MODEL taxirides.fare_model_551,(
  SELECT * FROM taxirides.report_prediction_data)
)

```
