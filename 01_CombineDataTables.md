
``` SQL
/*


Create a data table that contains all of the Cyclistic trip data.

Data for the months of May, June, July, August, September, and October

were split into 2 files to adhere to Google Drive's 100MB file size limit.


*/

  

CREATE TABLE cyclistic-capstone-494818.Cyclistic_Tripdata_2025.All_Tripdata AS (
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.01_Jan`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.02_Feb`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.03_Mar`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.04_Apr`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.05_May1`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.05_May2`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.06_Jun1`	
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.06_Jun2`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.07_Jul1`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.07_Jul2`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.08_Aug1`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.08_Aug2`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.09_Sep1`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.09_Sep2`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.10_Oct1`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.10_Oct1`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.11_Nov`
	UNION ALL
	SELECT * FROM `cyclistic-capstone-494818.Cyclistic_Tripdata_2025.12_Dec`
);
```