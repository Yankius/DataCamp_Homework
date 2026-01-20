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
