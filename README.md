# Uber Trip Analysis Project

🚖 Dive into the Uber trip data! This project explores **ride patterns, vehicle performance, cancellations, customer behavior, and revenue trends**, uncovering key insights to improve operations and business decisions.

🔍 SQL queries? Check them out here: [project_sql folder](/Project_sql/)

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
