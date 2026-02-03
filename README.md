MODULE 2 





























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
