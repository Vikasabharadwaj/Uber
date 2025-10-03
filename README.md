# Uber Trip Analysis Project

🚖 Dive into the Uber trip data! This project explores **ride patterns, vehicle performance, cancellations, customer behavior, and revenue trends**, uncovering key insights to improve operations and business decisions.

🔍 SQL queries? Check them out here: [project sql folder](/Sql/Sql_Querries.sql/)

---

## Background

This project was designed to analyze Uber trip data to understand:

- How different **vehicle types perform** in terms of distance and revenue  
- **Customer satisfaction** through ratings  
- **Ride cancellations** from customers and drivers  
- **Payment method adoption**, e.g., UPI usage  
- **Operational performance** to identify inefficiencies  

The insights also serve as the foundation for **Power BI dashboards**, where trends, patterns, and KPIs can be visualized dynamically.

### Questions answered through SQL and Power BI

1. How many rides were successfully completed?  
2. What is the **average distance per vehicle type**?  
3. How many rides were cancelled by customers or drivers?  
4. Who are the top customers by ride count?  
5. What are the **max/min driver ratings** per vehicle type?  
6. How do customers rate different vehicle types?  
7. What is the **total revenue** from completed rides?  
8. Which rides used **UPI payments**?  
9. What are the reasons for **incomplete rides**?  

---

## Tools I Used

- **SQL:** Core for querying Uber trip data  
- **PostgreSQL:** Database management system for handling datasets  
- **Visual Studio Code:** Writing and executing SQL scripts  
- **Power BI:** For building interactive dashboards and visualizing insights  
- **Git & GitHub:** Version control and project sharing  

---

## The Analysis

Each SQL query was designed to extract meaningful insights from Uber trip data.

### 1. Successful Rides

```sql
SELECT * 
FROM Trip_Details
WHERE Ride_Status = 'Success';
```
Provides details of successfully completed trips.
Helps track business success rate.
Insight: Completed rides reflect operational efficiency and customer engagement.

### 2. Average Ride Distance per Vehicle Type

```sql
SELECT 
    Vehicle_Type, 
    ROUND(AVG(Distance_km), 2)::text || ' km' AS avg_distance
FROM Trip_Details
GROUP BY Vehicle_Type;
```
Shows which vehicles are preferred for longer or shorter trips.
Insight: Sedans and SUVs usually cover longer distances; Bikes and Autos mostly handle short city rides.

### 3. Customer Cancellations
```sql
SELECT COUNT(*) AS cancelled_by_customers
FROM Trip_Details
WHERE Ride_Status = 'Cancelled by Customer';
```
Helps understand customer behavior and dissatisfaction patterns.
Insight: High cancellations may indicate pricing issues, delays, or user experience problems.

### 4. Top 5 Customers by Ride Count

```sql
SELECT Customer_ID, COUNT(Ride_ID) AS total_rides
FROM Trip_Details
GROUP BY Customer_ID
ORDER BY total_rides DESC
LIMIT 5;
```

Identifies the most loyal/high-value customers.
Insight: Top customers can be targeted with loyalty rewards or premium offers.

### 5.Driver Cancellations

```sql
SELECT COUNT(*) AS cancelled_by_driver
FROM Trip_Details
WHERE Driver_Cancellations = 'Personal & Car related issue';
```

Highlights operational inefficiencies due to driver issues.
Insight: Monitoring driver cancellations helps optimize driver management.


# Power BI Analysis (DAX Measures)

This section summarizes the **Power BI measures** used in the Uber project, along with their **DAX formulas** and purpose.

---

## Revenue & Booking Measures

| Measure | DAX Formula | Purpose |
|---------|-------------|---------|
| **TotalBookings** | `TotalBookings = COUNTROWS('Trip_Details')` | Total number of rides/bookings. |
| **Total_Trips** | `Total_Trips = COUNTROWS('Trip_Details')` | Alias for total rides. |
| **Total_Booking_Amount** | `Total_Booking_Amount = SUM('Trip_Details'[Ride_Fare])` | Total revenue from all trips. |
| **Avg_Booking_Amount** | `Avg_Booking_Amount = AVERAGE('Trip_Details'[Ride_Fare])` | Average fare per ride. |

---

## Distance Measures

| Measure | DAX Formula | Purpose |
|---------|-------------|---------|
| **Total_Trip_Distance** | `Total_Trip_Distance = SUM('Trip_Details'[Distance_km])` | Total km traveled across all trips. |
| **Total_Trip_Distance_Display** | `Total_Trip_Distance_Display = FORMAT([Total_Trip_Distance], "#,##0") & " km"` | Formatted total distance for dashboard display. |
| **Avg_Trip_Distance** | `Avg_Trip_Distance = AVERAGE('Trip_Details'[Distance_km])` | Average distance per trip. |

---

## Trip Duration & Type

| Measure | DAX Formula | Purpose |
|---------|-------------|---------|
| **Avg_Trip_Time_Display** | `Avg_Trip_Time_Display = AVERAGE('Trip_Details'[Trip_Time_Minutes])` | Average trip duration in minutes. |
| **Trip_Type** | `Trip_Type = SELECTEDVALUE('Trip_Details'[Vehicle_Type])` | Displays the vehicle type selected in slicers/filters. |

---

## Cancellation Measures

| Measure | DAX Formula | Purpose |
|---------|-------------|---------|
| **CancledBookings** | `CancledBookings = CALCULATE(COUNTROWS('Trip_Details'), 'Trip_Details'[Ride_Status] = "Cancelled by Customer")` | Number of rides cancelled by customers. |
| **CancelledPercentage** | `CancelledPercentage = DIVIDE([CancledBookings], [TotalBookings], 0) * 100` | Percentage of rides cancelled. |

---

## Customer Behavior & Locations

| Measure | DAX Formula | Purpose |
|---------|-------------|---------|
| **Most_Frequent_Pickup** | `Most_Frequent_Pickup = TOPN(1, SUMMARIZE('Trip_Details', 'Trip_Details'[Pickup_Location], "Trips", COUNTROWS('Trip_Details')), [Trips], DESC)` | Most common pickup location. |
| **Most_Frequent_Drop** | `Most_Frequent_Drop = TOPN(1, SUMMARIZE('Trip_Details', 'Trip_Details'[Drop_Location], "Trips", COUNTROWS('Trip_Details')), [Trips], DESC)` | Most common drop location. |
| **Farthest_Trip** | `Farthest_Trip = MAX('Trip_Details'[Distance_km])` | Longest trip distance in the dataset. |


