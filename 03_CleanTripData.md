
``` SQL
/*

We want to clean the data. Data we need to remove from dataset:

- any trips less than a minute or longer than a day (can assume that these rides are outliers or mistakes of some kind)

- any trips that contain NULL values in any part of the column

- add day_of_week column

- add month column

*/

  

CREATE TABLE cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data AS (
	SELECT
		ride_id,
		rideable_type,
		started_at,
		ended_at,
		ride_length_in_mins,
		CASE
			EXTRACT(MONTH FROM started_at)
			WHEN 1 THEN 'January'
			WHEN 2 THEN 'February'
			WHEN 3 THEN 'March'
			WHEN 4 THEN 'April'
			WHEN 5 THEN 'May'
			WHEN 6 THEN 'June'
			WHEN 7 THEN 'July'
			WHEN 8 THEN 'August'
			WHEN 9 THEN 'September'
			WHEN 10 THEN 'October'
			WHEN 11 THEN 'November'
			WHEN 12 THEN 'December'
		END AS month,
		CASE EXTRACT(DAYOFWEEK FROM started_at)
			WHEN 1 THEN 'Sunday'
			WHEN 2 THEN 'Monday'
			WHEN 3 THEN 'Tuesday'
			WHEN 4 THEN 'Wednesday'
			WHEN 5 THEN 'Thursday'
			WHEN 6 THEN 'Friday'
			WHEN 7 THEN 'Saturday'
		END AS day_of_week,
		start_station_name,
		start_station_id,
		end_station_name,
		end_station_id,
		start_lat,
		start_lng,
		end_lat,
		end_lng,
		member_casual
	FROM
		`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata` AS main_table
	JOIN (
		SELECT
			ride_id,
			TIMESTAMP_DIFF(ended_at, started_at, MINUTE) AS ride_length_in_mins
		FROM 
			`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata`) AS table1
		USING(ride_id)
		WHERE
		ride_length_in_mins > 1 AND ride_length_in_mins < 1440 AND
		start_station_name IS NOT NULL AND
		start_station_id IS NOT NULL AND
		end_station_name IS NOT NULL AND
		end_station_id IS NOT NULL AND
		start_lat IS NOT NULL AND
		start_lng IS NOT NULL AND
		end_lat IS NOT NULL AND
		end_lng IS NOT NULL
);
```