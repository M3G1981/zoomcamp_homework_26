MODULE 3 HOMEWORK
Q 1 20,332,093
Q 2 0 MB for the External Table and 155.12 MB for the Materialized Table
Q 3 BigQuery is a columnar database, and it only scans the specific columns requested in the query. Querying two columns (PULocationID, DOLocationID) requires reading more data than querying one column (PULocationID), leading to a higher estimated number of bytes processed.
Q 4 SELECT COUNT(*)
FROM dtc-de-zoomcamp-040473.zoomcamp.yellow_taxi_native
WHERE fare_amount = 0;
Answer = 8333
Q 5 Partition by tpep_dropoff_datetime and Cluster on VendorID
Q 6 310.24 MB for non-partitioned table and 26.84 MB for the partitioned table
SELECT DISTINCT VendorID 
FROM `dtc-de-zoomcamp-040473.zoomcamp.yellow_taxi_partitioned`
WHERE tpep_dropoff_datetime Between '2024-03-01' AND '2024-03-15'
Q 7 GCP Bucket
Q 8 False
Q 9 0bytes (we ran the query at the start of the homework and the results was cached 


MODULE 2 
Q 1 128.3 MiB
Q 2 green_tripdata_2020-04.csv
Q 3 select count(*) from yellow_tripdata
Q 4 select count(*) from green_tripdata
Q 5 meganhendricks@MacBook-Air-3 KESTRA  % curl -L -o yellow_tripdata_2021-03.csv.gz \
https://github.com/DataTalksClub/nyc-tlc-data/releases/download/yellow/yellow_tripdata_2021-03.csv.gz

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
100 33.5M  100 33.5M    0     0  3649k      0  0:00:09  0:00:09 --:--:-- 3775k
meganhendricks@MacBook-Air-3 KESTRA  % gunzip yellow_tripdata_2021-03.csv.gz

meganhendricks@MacBook-Air-3 KESTRA  % wc -l yellow_tripdata_2021-03.csv

 1925153 yellow_tripdata_2021-03.csv
meganhendricks@MacBook-Air-3 KESTRA  % 
Q 6 Add a timezone property set to America/New_York in the Schedule trigger configuration
IANA


























MODULE 1

ANSWER 1 
docker run -it --rm --entrypoint=bash python:3.13
pip --version
pip 25.3

ANSWER 2 db:5432

ANSWER 3 
Select Count(*)
FROM "green_taxi_data"
WHERE "lpep_pickup_datetime" >= '2025-11-01' AND "lpep_pickup_datetime" < '2025-12-01'
AND "trip_distance" <=1;
8007

Answer 4
SELECT "trip_distance", "lpep_pickup_datetime"
FROM "green_taxi_data"
WHERE "trip_distance" >0 AND "trip_distance" <100
Order By "trip_distance" DESC;
2025-11-14 15:36:27

Answer 5
SELECT SUM(t.total_amount)as total,z."Zone"
FROM "green_taxi_data" AS "t"
Join "zones" AS "z" on t."PULocationID" = z."LocationID"
WHERE t."lpep_pickup_datetime" >='2025-11-18' AND t."lpep_pickup_datetime" < '2025-11-19'
Group By z."Zone"
ORDER BY "total" DESC;
East Harlem South

Answer 6
SELECT
  zd."Zone" AS dropoff_zone,
  MAX(t.tip_amount) AS max_tip
FROM green_taxi_data AS t
JOIN zones AS zp
  ON t."PULocationID" = zp."LocationID"
JOIN zones AS zd
  ON t."DOLocationID" = zd."LocationID"
WHERE zp."Zone" = 'East Harlem North'
  AND t."lpep_pickup_datetime" >= '2025-11-01'
  AND t."lpep_pickup_datetime" <  '2025-12-01'
GROUP BY zd.zone
ORDER BY max_tip DESC
LIMIT 1;
Yorkville West
