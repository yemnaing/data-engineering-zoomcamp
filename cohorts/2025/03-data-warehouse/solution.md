CREATE SCHEMA `terraform-demo-449305.yellow_taxi_data`
OPTIONS(location='US'); -- Change location if needed


CREATE OR REPLACE EXTERNAL TABLE `terraform-demo-449305.yellow_taxi_data.external_yellow_taxi`
OPTIONS (
  format = 'PARQUET',
  uris = ['gs://gcs-buckets-ymn/*.parquet']
);

SELECT COUNT(*) FROM `terraform-demo-449305.yellow_taxi_data.yellow_taxi_trips`;

SELECT schema_name 
FROM `terraform-demo-449305`.INFORMATION_SCHEMA.SCHEMATA;


SELECT table_name 
FROM `terraform-demo-449305.yellow_taxi_data`.INFORMATION_SCHEMA.TABLES;


CREATE OR REPLACE TABLE `terraform-demo-449305.yellow_taxi_data.yellow_taxi_trips` AS
SELECT * FROM `terraform-demo-449305.yellow_taxi_data.external_yellow_taxi`;


SELECT COUNT(*) FROM `terraform-demo-449305.yellow_taxi_data.yellow_taxi_trips`;

SELECT COUNT(DISTINCT PULocationID) 
FROM `terraform-demo-449305.yellow_taxi_data.external_yellow_taxi`;

SELECT COUNT(DISTINCT PULocationID) 
FROM `terraform-demo-449305.yellow_taxi_data.yellow_taxi_trips`;


SELECT COUNT(*) AS fare_amount_zero_count
FROM `terraform-demo-449305.yellow_taxi_data.external_yellow_taxi`
WHERE fare_amount = 0;

SELECT DISTINCT VendorID
FROM `terraform-demo-449305.yellow_taxi_data.yellow_taxi_trips`
WHERE tpep_dropoff_datetime BETWEEN '2024-03-01' AND '2024-03-15';

SELECT DISTINCT VendorID
FROM `terraform-demo-449305.yellow_taxi_data.external_yellow_taxi`
WHERE tpep_dropoff_datetime BETWEEN '2024-03-01' AND '2024-03-15';


