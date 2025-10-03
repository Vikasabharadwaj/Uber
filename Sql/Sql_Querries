/*
Question: Retrieve all successful bookings
- Filter the rides where status is marked as 'Success'
- Provide details of successful trips only.
- Why? Helps identify completed rides and measure business success rate.
*/

SELECT * 
FROM Trip_Details
WHERE Ride_Status = 'Success';

/*
These are the rides that were successfully completed. 
This helps in measuring how many trips ended without cancellations.

[
  {
    "Ride_ID": "CNR7153255142",
    "Customer_ID": "CID713523",
    "Vehicle_Type": "Prime Sedan",
    "Ride_Fare": "444",
    "Ride_Status": "Success"
  },
  {
    "Ride_ID": "CNR7153255143",
    "Customer_ID": "CID713524",
    "Vehicle_Type": "Bike",
    "Ride_Fare": "158",
    "Ride_Status": "Success"
  }
]
*/

----------------------------------------------------------

/*
Question: Find the average ride distance for each vehicle type
- Group trips by vehicle type
- Calculate average distance per vehicle type
- Why? Shows which vehicles are preferred for longer or shorter trips.
*/

SELECT 
    Vehicle_Type, 
    ROUND(AVG(Distance_km), 2)::text || ' km' AS avg_distance
FROM Trip_Details
GROUP BY Vehicle_Type;


/*
Sedans and SUVs tend to have longer average distances, 
while Autos and Minis are mostly for short city rides.

[
  {
    "Vehicle_Type": "Auto",
    "avg_distance": "10 km"
  },
  {
    "Vehicle_Type": "Bike",
    "avg_distance": "25 km"
  },
  {
    "Vehicle_Type": "E-Bike",
    "avg_distance": "25 km"
  },
  {
    "Vehicle_Type": "Mini",
    "avg_distance": "25 km"
  },
  {
    "Vehicle_Type": "Prime Plus",
    "avg_distance": "25 km"
  },
  {
    "Vehicle_Type": "Prime Sedan",
    "avg_distance": "25 km"
  },
  {
    "Vehicle_Type": "Prime SUV",
    "avg_distance": "25 km"
  }
]
*/

----------------------------------------------------------

/*
Question: Get the total number of rides cancelled by customers
- Count all rides where ride status = 'Cancelled by Customer'
- Why? Useful to understand customer behavior and dissatisfaction patterns.
*/

SELECT COUNT(*) AS cancelled_by_customers
FROM Trip_Details
WHERE Ride_Status = 'Cancelled by Customer';

/*
This reveals how often customers cancel. 
A high number suggests dissatisfaction, delays, or pricing issues.

[
  {
    "cancelled_by_customers": "10500"
  }
]
*/

----------------------------------------------------------

/*
Question: List the top 5 customers with the highest number of rides
- Group by customer ID and count rides
- Order by ride count and return top 5
- Why? Helps identify most loyal/high-value customers.
*/

SELECT Customer_ID, COUNT(Ride_ID) AS total_rides
FROM Trip_Details
GROUP BY Customer_ID
ORDER BY total_rides DESC
LIMIT 5;

/*
These are the customers with the highest ride frequency, 
potentially good candidates for loyalty rewards or premium offers.

[
  {
    "Customer_ID": "CID785112",
    "total_rides": "80225"
  },
  {
    "Customer_ID": "CID308763",
    "total_rides": "6281"
  },
  {
    "Customer_ID": "CID734557",
    "total_rides": "6177"
  }
  {,
    "Customer_ID": "CID353074",
    "total_rides": "6110"
  },
  {
    "Customer_ID": "CID836942",
    "total_rides": "6019"
  }
]
*/

----------------------------------------------------------

/*
Question: Get the number of rides cancelled by drivers due to personal & car issues
- Filter where Driver_Cancellations = 'Personal & Car related issue'
- Why? Helps track driver reliability and maintenance-related problems.
*/

SELECT COUNT(*) AS cancelled_by_driver
FROM Trip_Details
WHERE Driver_Cancellations = 'Personal & Car related issue';

/*
This highlights how many rides failed due to driver-side issues. 
A high count can indicate operational inefficiency.

[
  {
    "cancelled_by_driver": "6542"
  }
]
*/

----------------------------------------------------------

/*
Question: Find the maximum and minimum driver ratings for Prime Sedan rides
- Filter by vehicle type = 'Prime Sedan'
- Get MAX and MIN driver ratings
- Why? Understand driver performance variation within premium service rides.
*/

SELECT MAX(Driver_Rating) AS max_rating,
       MIN(Driver_Rating) AS min_rating
FROM Trip_Details
WHERE Vehicle_Type = 'Prime Sedan';

/*
Prime Sedan drivers generally maintain high ratings, 
but minimum rating highlights service inconsistency.

[
  {
    "max_rating": "5",
    "min_rating": "3"
  }
]
*/

----------------------------------------------------------

/*
Question: Retrieve all rides where payment was made using UPI
- Filter Payment_Type = 'UPI'
- Why? Identifies adoption of digital payments.
*/

SELECT * 
FROM Trip_Details
WHERE Payment_Type = 'UPI';

/*
UPI is becoming one of the most popular methods for quick cashless payments. 
This result shows all such rides.

[
  {
    "Ride_ID": "CNR2982357879",
    "Customer_ID": "CID270156",
    "Payment_Type": "UPI",
    "Ride_Fare": "384"
  }
]
*/

----------------------------------------------------------

/*
Question: Find the average customer rating per vehicle type
- Group rides by vehicle type
- Calculate average rating given by customers
- Why? Helps evaluate customer satisfaction by ride type.
*/

SELECT Vehicle_Type, AVG(Customer_Rating) AS avg_customer_rating
FROM Trip_Details
GROUP BY Vehicle_Type;

/*


[
  {
    "Vehicle_Type": "Auto",
    "avg_distance": "4.00"
  },
  {
    "Vehicle_Type": "Bike",
    "avg_distance": "3.99"
  },
  {
    "Vehicle_Type": "E-Bike",
    "avg_distance": "3.99"
  },
  {
    "Vehicle_Type": "Mini",
    "avg_distance": "4.00"
  },
  {
    "Vehicle_Type": "Prime Plus",
    "avg_distance": "4.01"
  },
  {
    "Vehicle_Type": "Prime Sedan",
    "avg_distance": "4.00"
  },
  {
    "Vehicle_Type": "Prime SUV",
    "avg_distance": "4.00"
  }
]
*/

----------------------------------------------------------

/*
Question: Calculate the total booking value of successfully completed rides
- Filter Ride_Status = 'Success'
- Sum the ride fares
- Why? Shows overall revenue from completed trips.
*/

SELECT SUM(Ride_Fare) AS total_successful_ride_value
FROM Trip_Details
WHERE Ride_Status = 'Success';

/*
This represents total revenue generated from completed rides only.

[
  {
    "total_successful_ride_value": "984532"
  }
]
*/

----------------------------------------------------------

/*
Question: List all incomplete rides along with the reason
- Filter where Incomplete_Rides = 'Yes'
- Retrieve Ride_ID and Incomplete_Reason
- Why? Helps understand why rides fail and improve service reliability.
*/

SELECT Ride_ID, Incomplete_Reason
FROM Trip_Details
WHERE Incomplete_Rides = 'Yes';

/*
This provides insights into ride failures like network issues, 
driver unavailability, or customer no-shows.

[
  {
    "Ride_ID": "CNR2395710036",
    "Incomplete_Reason": "Canceled by Customer"
  },
  {
    "Ride_ID": "CNR6387231274",
    "Incomplete_Reason": "Canceled by Driver"
  }
]
*/
