# DataCamp_Homework
This is my data engineering homework submission repository

## Homework 1
### Question 1:
 **Answer:** pip vesrion is 25.3

### Question 2.
**Answer:**
- postgres:5432
- db:5432

### Question 3.
**Answer**: 8007

SQL Code:
```
SELECT 
   count('trip_distance')
FROM 
    public."green-taxi-data" t

WHERE 
    t.lpep_pickup_datetime::DATE >= '2025-11-01' AND  t.lpep_pickup_datetime::DATE<'2025-12-01'
	and
	trip_distance <=1;
```

### Question 4. 
**Answer:** 2025-11-14 
```
SELECT 
   t.lpep_pickup_datetime, 
   trip_distance
FROM 
    public."green-taxi-data" t
WHERE 
    t.lpep_pickup_datetime >= '2025-11-01' 
    AND t.lpep_pickup_datetime < '2025-12-01'
    AND trip_distance < 100


ORDER BY
    t.trip_distance DESC
LIMIT 1;
```


### Question 5
**Answer:** East Harlem North
```
SELECT 
    zpu."Zone", 
    SUM(t."total_amount")
FROM 
    public."green-taxi-data" t
JOIN 
    public."taxi-zones-lookup" zpu 
    ON t."PULocationID" = zpu."LocationID" 
WHERE 
    t.lpep_pickup_datetime::DATE = '2025-11-18'
GROUP BY 
    zpu."Zone"
ORDER BY 
    SUM(t."total_amount") DESC;
```	
	
### Question 6
**Answer:** LaGuardia Airport
```
SELECT 
    zpu."Zone", 
    SUM(t."tip_amount")
FROM 
    public."green-taxi-data" t
JOIN 
    public."taxi-zones-lookup" zpu 
    ON t."DOLocationID" = zpu."LocationID" 
WHERE 
    t.lpep_pickup_datetime::DATE >= '2025-11-01' AND  t.lpep_pickup_datetime::DATE<'2025-12-01'
GROUP BY 
    zpu."Zone"
ORDER BY 
    SUM(t."tip_amount") DESC;
```

## Homework 2
### Question 1:
 **Answer:** 128.3 MiB
### Question 2:
 **Answer:** green_tripdata_2020-04.csv
### Question 3:
 **Answer:** 24,648,499
 ```
select count(*)
from public.yellow_tripdata
WHERE DATE_PART('year', tpep_pickup_datetime) = 2020;
```
### Question 4:
 **Answer:** 1,734,051
 ```
select count(*)
from public.green_tripdata
WHERE DATE_PART('year', lpep_pickup_datetime) = 2020;
```
### Question 5:
 **Answer:** 1,925,152
 ```
select count(*)
from public.yellow_tripdata
WHERE DATE_PART('year', tpep_pickup_datetime) = 2021 and DATE_PART('month', tpep_pickup_datetime) = 3 ;
```
### Question 6:
 **Answer:** Add a timezone property set to America/New_York in the Schedule trigger configuration

 ## Homework 3
### Question 1:
 **Answer:** 20,332,093
'''
SELECT count(*) FROM `arched-memory-483623-k2.yellow_taxi_dataset.yellow_taxi_native` where extract(YEAR from tpep_pickup_datetime) = 2024;
'''
### Question 2:
  **Answer:** 0 MB for the External Table and 155.12 MB for the Materialized Table
  ```
SELECT count(distinct PULocationID) FROM `arched-memory-483623-k2.yellow_taxi_dataset.yellow-taxi-tables` 0bytes estimated

SELECT count(distinct PULocationID)  FROM `arched-memory-483623-k2.yellow_taxi_dataset.yellow_taxi_native`  155.12	MB estimated
```

### Question 3:
 **Answer:** BigQuery is a columnar database, and it only scans the specific columns requested in the query. Querying two columns (PULocationID, DOLocationID) requires reading more data than querying one column (PULocationID), leading to a higher estimated number of bytes processed.
 ```
SELECT PULocationID, DOLocationID FROM `arched-memory-483623-k2.yellow_taxi_dataset.yellow_taxi_native` 
```


### Question 4:
 **Answer:** 8,333
 ```
SELECT count (fare_amount) FROM `arched-memory-483623-k2.yellow_taxi_dataset.yellow-taxi-tables` where fare_amount = 0
```

### Question 5:
 **Answer:** Partition by tpep_dropoff_datetime and Cluster on VendorID

### Question 6:
 **Answer:** 310.24 MB for non-partitioned table and 26.84 MB for the partitioned table

 Reuse previous table and then create a partitioned table usig:
 ```
CREATE TABLE `arched-memory-483623-k2.yellow_taxi_dataset.optimized_taxi_data`
PARTITION BY DATE(tpep_dropoff_datetime)
CLUSTER BY VendorID
AS
SELECT * FROM `arched-memory-483623-k2.yellow_taxi_dataset.yellow-taxi-tables`;
```

### Question 7:
 **Answer:** GCP Bucket

 ### Question 8:
 **Answer:** False
 
 


 
