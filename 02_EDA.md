![[Screenshot 2026-04-30 at 4.00.55 PM.png|232]]

``` SQL
/*
EDA: Number of NULL values in each column
*/

SELECT
	COUNT(*) - COUNT(ride_id) AS ride_id,
	COUNT(*) - COUNT(rideable_type) AS rideable_type,
	COUNT(*) - COUNT(started_at) AS started_at,
	COUNT(*) - COUNT(ended_at) AS ended_at,
	COUNT(*) - COUNT(start_station_name) AS start_station_name,
	COUNT(*) - COUNT(start_station_id) AS start_station_id,
	COUNT(*) - COUNT(end_station_name) AS end_station_name,
	COUNT(*) - COUNT(end_station_id) AS end_station_id,
	COUNT(*) - COUNT(start_lat) AS start_lat,
	COUNT(*) - COUNT(start_lng) AS start_lng,
	COUNT(*) - COUNT(end_lat) AS end_lat,
	COUNT(*) - COUNT(end_lng) AS end_lng,
	COUNT(*) - COUNT(member_casual) AS member_casual
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`;
```

RESULT

| ride_id | rideable_type | started_at | ended_at | start_station_name | start_station_id | end_station_name | end_station_id | start_lat | start_lng | end_lat | end_lng | member_casual |
| ------- | ------------- | ---------- | -------- | ------------------ | ---------------- | ---------------- | -------------- | --------- | --------- | ------- | ------- | ------------- |
| 0       | 0             | 0          | 0        | 1120411            | 1120411          | 1109205          | 1109205        | 0         | 0         | 5194    | 5194    | 0             |
``` SQL
/*

EDA: Check for the number of rides greater than a day or less than 1 minute

*/

SELECT
	COUNT(*) AS num_rides
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`
WHERE
	TIMESTAMP_DIFF(ended_at, started_at, MINUTE) > 1440 OR 
	TIMESTAMP_DIFF(ended_at, started_at, MINUTE) < 1;
```

RESULT:
num_rides
142799

``` SQL
/*

EDA: Check Min, Max, and Mean of Ride Length

*/

SELECT
	MIN(TIMESTAMP_DIFF(ended_at, started_at, MINUTE)) AS ride_length_minutes_min,
	MAX(TIMESTAMP_DIFF(ended_at, started_at, MINUTE)) AS ride_length_minutes_max,
	AVG(TIMESTAMP_DIFF(ended_at, started_at, MINUTE)) AS ride_length_minutes_mean
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`
WHERE
	TIMESTAMP_DIFF(ended_at, started_at, MINUTE) IS NOT NULL;
```

RESULT:

| ride_length_minutes_min | ride_length_minutes_max | ride_length_minutes_mean |
| ----------------------- | ----------------------- | ------------------------ |
| -54                     | 1574                    | 15.536598817265908       |

``` SQL
/*

EDA: Check Min, Max, and Mean of Ride Length

*/

SELECT
	MIN(TIMESTAMP_DIFF(ended_at, started_at, SECOND)) AS ride_length_seconds_min,
	MAX(TIMESTAMP_DIFF(ended_at, started_at, SECOND)) AS ride_length_seconds_max,
	AVG(TIMESTAMP_DIFF(ended_at, started_at, SECOND)) AS ride_length_seconds_mean
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`
WHERE
	TIMESTAMP_DIFF(ended_at, started_at, SECOND) IS NOT NULL;
```

RESULT:

| ride_length_seconds_min | ride_length_seconds_max | ride_length_seconds_mean |
| ----------------------- | ----------------------- | ------------------------ |
| -3287                   | 94494                   | 961.45991346260814       |

``` SQL
/*
EDA: Check the rideable_type & member_casual for unique values
*/

SELECT DISTINCT
	rideable_type,
	member_casual
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`;
```
RESULT:

| rideable_type | member_casual |
| ------------- | ------------- |
| classic_bike  | casual        |
| electric_bike | member        |

``` SQL
/*

EDA: Make sure ride_id length is only 16 characters long

*/
  
SELECT
	LENGTH(TRIM(ride_id)) AS ride_id_length,
	COUNT(*) AS ride_count
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`
GROUP BY
	ride_id_length
ORDER BY
	ride_count DESC;
```

INITIAL RESULTS:

| ride_id_length | ride_count |
| -------------- | ---------- |
| 16             | 5551470    |
| 18             | 257        |
| 19             | 186        |
| 17             | 69         |
| 20             | 35         |
| 5              | 24         |
| 14             | 2          |
| 25             | 2          |
| 15             | 2          |
| 70             | 2          |
| 73             | 1          |
| 23             | 1          |
``` SQL
/*
EDA: Finding the rides that have ride_id's that are not 16 characters
*/

SELECT
	ride_id
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`
WHERE
	LENGTH(ride_id) = [character length];
```

``` SQL
/*
EDA: Counts of every starting station
*/

SELECT
	DISTINCT start_station_name,
	COUNT(*) AS start_station_count
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`
GROUP BY
	start_station_name;
```

``` SQL
/*
EDA: Count of null starting station
*/

SELECT
	COUNT(*) AS null_start_station
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`
WHERE
	start_station_name IS NULL;
```
RESULT:

| null_start_station |
| ------------------ |
| 1120411            |
``` SQL
/*
EDA: Count of null ending station
*/

SELECT
	COUNT(*) AS null_end_station
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`
WHERE
	end_station_name IS NULL;
```
RESULT:

| null_end_station |
| ---------------- |
| 1109205          |
|                  |

``` SQL
/*
EDA: Average ride length of casual riders and member riders
*/

SELECT
	member_casual,
	AVG(TIMESTAMP_DIFF(ended_at, started_at, MINUTE)) AS avg_ride_length_min
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`
GROUP BY
	member_casual;
```
RESULT:

| member_casual | avg_ride_length_min |
| ------------- | ------------------- |
| casual        | 22.081376582110956  |
| member        | 11.899265671795726  |

``` SQL
/*
EDA: Total number of casual and member rides
*/

SELECT
	member_casual,
	COUNT(member_casual) AS total_riders
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`
GROUP BY
	member_casual;
```
RESULT:

| member_casual | total_riders |
| ------------- | ------------ |
| casual        | 1983347      |
| member        | 3568704      |

``` SQL
/*
EDA: Total number of rides per rideable_type
*/

SELECT
	rideable_type,
	COUNT(rideable_type) AS total_rides
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`
GROUP BY
	rideable_type;
```
RESULT:

| rideable_type | total_rides |
| ------------- | ----------- |
| classic_bike  | 2007694     |
| electric_bike | 3544357     |

``` SQL
/*
EDA: rideable_type by member_casual
*/

SELECT
	SUM(CASE WHEN rideable_type = 'electric_bike' THEN 1 ELSE 0 END) AS electric_count,
	
	SUM(CASE WHEN rideable_type = 'classic_bike' THEN 1 ELSE 0 END) AS classic_count,
	
	SUM(CASE WHEN member_casual = 'member' THEN 1 ELSE 0 END) AS member_count,
	
	SUM(CASE WHEN member_casual = 'casual' THEN 1 ELSE 0 END) AS casual_count,
	
	SUM(CASE WHEN (rideable_type = 'classic_bike' AND member_casual = 'member') 
		THEN 1 ELSE 0 END) AS classic_member_count,
	
	SUM(CASE WHEN (rideable_type = 'classic_bike' AND member_casual = 'casual') 
		THEN 1 ELSE 0 END) AS classic_casual_count,
	
	SUM(CASE WHEN (rideable_type = 'electric_bike' AND member_casual = 'member') 
		THEN 1 ELSE 0 END) AS electric_member_count,
	
	SUM(CASE WHEN (rideable_type = 'electric_bike' AND member_casual = 'casual') 
		THEN 1 ELSE 0 END) AS electric_casual_count

FROM
`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`;
```
RESULT:

| electric_count | classic_count | member_count | casual_count | classic_member_count | classic_casual_count | electric_member_count | electric_casual_count |
| -------------- | ------------- | ------------ | ------------ | -------------------- | -------------------- | --------------------- | --------------------- |
| 3544357        | 2007694       | 3568704      | 1983347      | 1321139              | 686555               | 2247565               | 1296792               |

More easily read tables:

| rideable_type | member_casual | total_rides |
| ------------- | ------------- | ----------- |
| electric_bike | casual        | 1296792     |
| classic_bike  | member        | 1321139     |
| classic_bike  | casual        | 686555      |
| electric_bike | member        | 2247565     |

| Type           | Count   |
| -------------- | ------- |
| electric_count | 3544357 |
| classic_count  | 2007694 |
| member_count   | 3568704 |
| casual_count   | 1983347 |


``` SQL
/*
EDA: Count of null values in start or end latitude or longitude (ie/ coordinates)
*/

SELECT
	COUNT(*) as total_coor_null
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`
WHERE
	start_lat IS NULL OR
	start_lng IS NULL OR
	end_lat IS NULL OR
	end_lng IS NULL;
```
RESULT:

|total_coor_null|
|-|
|5194|
