## Queries to perform

-- Number of rides per month
```SQL
SELECT
	COUNT(*) AS num_rides,
	month
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
GROUP BY
	month
ORDER BY
	num_rides DESC;
```
RESULT:

| num_rides | month     |
| --------- | --------- |
| 1071148   | October   |
| 502427    | August    |
| 481434    | July      |
| 455722    | September |
| 435629    | June      |
| 331539    | May       |
| 251151    | April     |
| 227713    | November  |
| 203325    | March     |
| 105859    | February  |
| 93326     | January   |
| 92627     | December  |

-- Number of rides per month, ordered by month
``` SQL
SELECT
	COUNT(*) AS num_rides,
	EXTRACT(MONTH FROM started_at) as month_num,
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
GROUP BY
	month_num
ORDER BY
	month_num ASC;
```
RESULT:

| num_rides | month_num |
| --------- | --------- |
| 93326     | 1 (Jan)   |
| 105859    | 2 (Feb)   |
| 203325    | 3 (Mar)   |
| 251151    | 4 (Apr)   |
| 331539    | 5 (May)   |
| 435629    | 6 (Jun)   |
| 481434    | 7 (Jul)   |
| 502427    | 8 (Aug)   |
| 455722    | 9 (Sep)   |
| 1071148   | 10 (Oct)  |
| 227713    | 11 (Nov)  |
| 92627     | 12 (Dec)  |

-- Busiest month & quarter of the year (highest number of rides per month)
``` SQL
SELECT
	COUNT(*) as num_rides,
	month
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
GROUP BY
	month
ORDER BY
	num_rides DESC
LIMIT 1;
```

`To find the busiest quarter, sum the months by quarter, then divide the number of rides in each quarter by 3 to find the avg number of rides per quarter.`

-- Busiest day of the week (average rides per day of the week)
```SQL
SELECT
	day_of_week,
	COUNT(*) AS num_rides
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
GROUP BY
	day_of_week
ORDER BY
	num_rides DESC;
```
RESULT:

| day_of_week | num_rides |
| ----------- | --------- |
| Friday      | 653517    |
| Thursday    | 645044    |
| Saturday    | 637871    |
| Wednesday   | 605985    |
| Tuesday     | 599097    |
| Monday      | 570087    |
| Sunday      | 540299    |


-- Station analysis (average busiest & slowest starting and ending stations)
``` SQL
SELECT
	start_station_name,
	COUNT(*) AS num_rides
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
GROUP BY
	start_station_name
ORDER BY
	num_rides DESC
LIMIT 10;
```
RESULT:

| start_station_name                 | num_rides |
| ---------------------------------- | --------- |
| DuSable Lake Shore Dr & Monroe St  | 39080     |
| Kingsbury St & Kinzie St           | 38719     |
| Navy Pier                          | 37042     |
| Michigan Ave & Oak St              | 33720     |
| DuSable Lake Shore Dr & North Blvd | 33406     |
| Clinton St & Washington Blvd       | 29943     |
| Canal St & Madison St              | 28384     |
| Clinton St & Madison St            | 28096     |
| Clark St & Elm St                  | 28017     |
| Millennium Park                    | 27097     |



-- Relationship between member_casual and rideable_type
``` SQL
SELECT
	member_casual,
	rideable_type,
	COUNT(*) AS num_rides
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
GROUP BY
	member_casual,
	rideable_type
ORDER BY
	num_rides DESC;
```
RESULT:

| member_casual | rideable_type | num_rides |
| ------------- | ------------- | --------- |
| member        | classic_bike  | 1475170   |
| member        | electric_bike | 1274250   |
| casual        | classic_bike  | 754043    |
| casual        | electric_bike | 748437    |


-- Relationship between day of the week and rideable_type
``` SQL
SELECT
	day_of_week,
	rideable_type,
	COUNT(*) AS num_rides
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
GROUP BY
	day_of_week,
	rideable_type
ORDER BY
	num_rides DESC;
```
RESULT:

| day_of_week | rideable_type | num_rides |
| ----------- | ------------- | --------- |
| Saturday    | classic_bike  | 352279    |
| Friday      | classic_bike  | 330639    |
| Thursday    | classic_bike  | 325349    |
| Friday      | electric_bike | 322878    |
| Thursday    | electric_bike | 319695    |
| Tuesday     | classic_bike  | 310449    |
| Wednesday   | classic_bike  | 305917    |
| Sunday      | classic_bike  | 303647    |
| Monday      | classic_bike  | 300933    |
| Wednesday   | electric_bike | 300068    |
| Tuesday     | electric_bike | 288648    |
| Saturday    | electric_bike | 285592    |
| Monday      | electric_bike | 269154    |
| Sunday      | electric_bike | 236652    |


-- Relationship between day of the week and member_casual
``` SQL
SELECT
	member_casual,
	day_of_week,
	COUNT(*) AS num_rides
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
GROUP BY
	member_casual,
	day_of_week
ORDER BY
	num_rides DESC;
```
RESULT:

| member_casual | day_of_week | num_rides |
| ------------- | ----------- | --------- |
| member        | Thursday    | 451948    |
| member        | Wednesday   | 441133    |
| member        | Tuesday     | 435181    |
| member        | Friday      | 410652    |
| member        | Monday      | 397090    |
| member        | Saturday    | 326643    |
| casual        | Saturday    | 311228    |
| member        | Sunday      | 286773    |
| casual        | Sunday      | 253526    |
| casual        | Friday      | 242865    |
| casual        | Thursday    | 193096    |
| casual        | Monday      | 172997    |
| casual        | Wednesday   | 164852    |
| casual        | Tuesday     | 163916    |

-- Relationship between month and rideable_type
``` SQL
SELECT
	month,
	rideable_type,
	COUNT(*) as num_rides
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
WHERE
	rideable_type = 'classic_bike'
GROUP BY
	month,
	rideable_type
ORDER BY
	num_rides DESC;
	
	
SELECT
	month,
	rideable_type,
	COUNT(*) as num_rides
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
WHERE
	rideable_type = 'electric_bike'
GROUP BY
	month,
	rideable_type
ORDER BY
	num_rides DESC;
```

| month     | rideable_type | num_rides |
| --------- | ------------- | --------- |
| October   | classic_bike  | 538297    |
| August    | classic_bike  | 275315    |
| July      | classic_bike  | 259371    |
| June      | classic_bike  | 248591    |
| September | classic_bike  | 234147    |
| May       | classic_bike  | 181617    |
| April     | classic_bike  | 134970    |
| November  | classic_bike  | 112080    |
| March     | classic_bike  | 108006    |
| February  | classic_bike  | 51068     |
| December  | classic_bike  | 43385     |
| January   | classic_bike  | 42366     |

| month     | rideable_type | num_rides |
| --------- | ------------- | --------- |
| October   | electric_bike | 532851    |
| August    | electric_bike | 227112    |
| July      | electric_bike | 222063    |
| September | electric_bike | 221575    |
| June      | electric_bike | 187038    |
| May       | electric_bike | 149922    |
| April     | electric_bike | 116181    |
| November  | electric_bike | 115633    |
| March     | electric_bike | 95319     |
| February  | electric_bike | 54791     |
| January   | electric_bike | 50960     |
| December  | electric_bike | 49242     |


-- Relationship between month and member_casual
``` SQL
SELECT
	month,
	member_casual,
	COUNT(*) AS trip_count
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
GROUP BY
	month,
	member_casual
ORDER BY
	trip_count DESC;
```

| month     | member_casual | trip_count |
| --------- | ------------- | ---------- |
| October   | member        | 722079     |
| October   | casual        | 349069     |
| September | member        | 286948     |
| August    | member        | 285868     |
| July      | member        | 277408     |
| June      | member        | 246628     |
| August    | casual        | 216559     |
| May       | member        | 208431     |
| July      | casual        | 204026     |
| June      | casual        | 189001     |
| April     | member        | 175762     |
| September | casual        | 168774     |
| November  | member        | 164972     |
| March     | member        | 143032     |
| May       | casual        | 123108     |
| February  | member        | 86657      |
| January   | member        | 77294      |
| April     | casual        | 75389      |
| December  | member        | 74341      |
| November  | casual        | 62741      |
| March     | casual        | 60293      |
| February  | casual        | 19202      |
| December  | casual        | 18286      |
| January   | casual        | 16032      |

-- Relationship between ride_length and member_casual
``` SQL
SELECT
	member_casual,
	AVG(ride_length_in_mins)
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
GROUP BY
	member_casual
```
RESULT

| member_casual | avg_ride_length_min |
| ------------- | ------------------- |
| casual        | 21.882243357648719  |
| member        | 12.238824552087301  |

-- Relationship between ride_length and rideable_type
``` SQL
SELECT
	rideable_type,
	AVG(ride_length_in_mins) AS avg_ride_length_min
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
GROUP BY
	rideable_type
```
RESULT

| rideable_type | avg_ride_length_min |
| ------------- | ------------------- |
| classic_bike  | 18.727010832971153  |
| electric_bike | 12.251428916090289  |

-- relationship between average ride length, member_casual, and month
``` SQL
SELECT
	rideable_type,
	month,
	AVG(ride_length_in_mins) AS avg_ride_length_min
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
GROUP BY
	rideable_type,
	month
ORDER BY
	rideable_type,
	avg_ride_length_min DESC;
```
RESULT:

| rideable_type | month     | avg_ride_length_min |
| ------------- | --------- | ------------------- |
| classic_bike  | July      | 21.289496512717324  |
| classic_bike  | June      | 21.16562546512143   |
| classic_bike  | August    | 20.899293536494568  |
| classic_bike  | May       | 19.321743008639054  |
| classic_bike  | September | 18.794014016835575  |
| classic_bike  | October   | 17.692931597240918  |
| classic_bike  | April     | 16.685707935096673  |
| classic_bike  | January   | 16.514799603455593  |
| classic_bike  | November  | 16.078140613847264  |
| classic_bike  | March     | 15.970936799807413  |
| classic_bike  | December  | 15.638538665437363  |
| classic_bike  | February  | 12.104742696013162  |
| electric_bike | August    | 14.245940329000666  |
| electric_bike | July      | 13.930488194791565  |
| electric_bike | June      | 13.689143382628123  |
| electric_bike | September | 13.064009928917974  |
| electric_bike | May       | 12.341624311308557  |
| electric_bike | October   | 11.673398379659591  |
| electric_bike | April     | 11.038526092906764  |
| electric_bike | March     | 10.794647446993785  |
| electric_bike | November  | 10.541151747338567  |
| electric_bike | December  | 9.4526826692660713  |
| electric_bike | January   | 8.9443681318681261  |
| electric_bike | February  | 8.66645982004342    |


-- Relationship between starting_station and member_casual
``` SQL
SELECT
	start_station_name,
	month,
	member_casual,
	COUNT(*) AS trip_count
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
WHERE
	member_casual = "casual"
GROUP BY
	start_station_name,
	month,
	member_casual
ORDER BY
	trip_count DESC
LIMIT 10;

SELECT
	start_station_name,
	month,
	member_casual,
	COUNT(*) AS trip_count
FROM
	`cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data`
WHERE
	member_casual = "member"
GROUP BY
	start_station_name,
	month,
	member_casual
ORDER BY
	trip_count DESC
LIMIT 10;
```

| start_station_name                | month     | member_casual | trip_count |
| --------------------------------- | --------- | ------------- | ---------- |
| Navy Pier                         | August    | casual        | 9856       |
| Navy Pier                         | October   | casual        | 8398       |
| Streeter Dr & Grand Ave           | June      | casual        | 7271       |
| Navy Pier                         | September | casual        | 6517       |
| Streeter Dr & Grand Ave           | July      | casual        | 6312       |
| DuSable Lake Shore Dr & Monroe St | October   | casual        | 5632       |
| DuSable Lake Shore Dr & Monroe St | August    | casual        | 5302       |
| DuSable Lake Shore Dr & Monroe St | July      | casual        | 4306       |
| Michigan Ave & Oak St             | August    | casual        | 4289       |
| DuSable Lake Shore Dr & Monroe St | June      | casual        | 4263       |


| start_station_name           | month   | member_casual | trip_count |
| ---------------------------- | ------- | ------------- | ---------- |
| Kingsbury St & Kinzie St     | October | member        | 7728       |
| University Ave & 57th St     | October | member        | 6992       |
| Clinton St & Washington Blvd | October | member        | 6024       |
| Ellis Ave & 55th St          | October | member        | 5808       |
| Clinton St & Madison St      | October | member        | 5193       |
| Ellis Ave & 60th St          | October | member        | 5092       |
| Canal St & Madison St        | October | member        | 4804       |
| State St & Chicago Ave       | October | member        | 4780       |
| Clinton St & Jackson Blvd    | October | member        | 4712       |
| Clark St & Elm St            | October | member        | 4324       |

``` SQL
/* Perform analysis finding and graphing the relationships between the variables */ 


cyclistic-capstone-494818.Cyclistic_Tripdata_2025.clean_trip_data
```