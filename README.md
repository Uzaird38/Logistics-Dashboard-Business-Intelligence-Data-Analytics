# Logistics-Dashboard-Business-Intelligence-Data-Analytics
A Power BI business intelligence project for monitoring logistics operations, delivery performance, customer satisfaction, hub efficiency, driver performance, and vehicle status.
## Project type: Business Intelligence / Data Analytics
Tool: Microsoft Power BI
Data format: CSV

## 1. Project Overview
The SwiftRoute Logistics Dashboard brings operational data from four datasets—Hubs, Drivers, Vehicles, and Orders—into an interactive report.

The goal is to help logistics teams answer questions such as:
- How many orders are being handled?
- What percentage of orders arrive on time?
- How satisfied are customers?
- Which hubs process the most orders, and which perform best?
- Which drivers have higher delay rates?
- What is the status of the vehicle fleet?
- How do delivery results change over time?
  The report contains three pages:
## 2. Logistics Overview
– a high-level view of orders, delivery KPIs, hubs, drivers, and vehicles.
<img width="1039" height="548" alt="Logistics Dashboard" src="https://github.com/user-attachments/assets/67522507-b096-43b7-8eed-cb187cdd7522" />
This page presents the overall operational picture, including:
- Total Orders
- On-Time Delivery Rate
- Customer Satisfaction Score (CSAT)
- Average Delivery Time
- Hub capacity and order volume
- Hub performance ranking
- Driver experience versus performance rating
- Drivers with the most delays
- Active and maintenance vehicle counts
- Orders by vehicle model

## 3. Drivers Overview 
– a closer look at driver experience, ratings, delivery delays, and individual driver trends.
<img width="1037" height="549" alt="Drivers Overview" src="https://github.com/user-attachments/assets/e43e2cb9-8a42-4ff8-8e41-e238510fcde1" />

This page focuses on driver-level analysis, including:
- Driver selection
- Driver name, hire date, and years of experience
- Performance rating
- Experience versus performance rating distribution
- Drivers with the most delays
- Monthly on-time delivery trend
The report includes Year and Month filters. The Drivers Overview page also includes a driver selector and a measure selector for the trend chart.
 
## 4. Hubs Overview
- a clear understanding of how hubs are performing overtime.
<img width="1031" height="540" alt="Hubs Overview" src="https://github.com/user-attachments/assets/394e7131-c320-4516-8bba-4988abe66844" />

## 5. Key Performance Indicators
  Total Orders: Number of orders represented by the selected dashboard context
  On-Time Delivery Rate: Share of orders delivered on time
  Customer Satisfaction (CSAT): Customer satisfaction result shown by the report
  Average Delivery Time:  Average delivery duration shown by the report
**Note:** KPI values depend on the selected Year, Month, and other report filters. They should be interpreted in the context of the filter selection, not as all-time company totals.
## 6. Dataset Description
   The project uses four CSV tables. The column descriptions below explain the likely business meaning of each field based on its name and its use in the dashboard.
  6.1 **Hubs table**
  Contains the logistics hub master data.
  6.2 **Drivers table**
  Contains driver information and performance attributes.
  6.3 **Vehicles table**
  Contains vehicle details and fleet-maintenance information.
  6.4 **Orders table**
  Contains order-level delivery and operational information. This is the central  transaction table for many of the report's delivery KPIs.

## 7. Data Model and Relationships
A sensible model for these four tables is a star-style structure, with Orders as the transaction table and the other tables providing descriptive attributes.
<img width="630" height="484" alt="image" src="https://github.com/user-attachments/assets/24476d92-6f54-46f8-a478-4372fa6e193d" />
## 8. Findings: 
The following are observations
 8.1 **Overall logistics findings – April 2024**
- The dashboard displays 1,156 total orders.
- The displayed on-time delivery rate is 80.5%. This suggests that roughly one in five orders did not meet the on-time condition, subject to the report's measure definition.
- The displayed customer satisfaction score is 84.2%.
- Average delivery time is 35.78 hours.
- The overview shows 6 hubs, 55 drivers, and 45 vehicles.
 8.2 **Hub performance – April 2024**
The Hub Performance Ranking visual shows the following percentages:
Houston Hub	     82.6%
Dallas Main Hub	 80.9%
El Paso Hub	     80.5%
San Antonio Hub	 79.8%
Fort Worth Hub	 79.3%
Austin Hub	     78.1%
Houston Hub has the highest displayed performance at 82.6%.
Austin Hub has the lowest displayed performance at 78.1% among the six hubs shown for the selected filters.

 8.3 **Vehicle status – April 2024**
The vehicle status visual shows:
- 45 vehicles in total.
- 33 Active vehicles (73.33%).
- 12 Maintenance vehicles (26.67%).
This indicates that just under three-quarters of the displayed fleet is marked Active, while a little over one-quarter is marked Maintenance.

 8.4 **Interpretation and business opportunities**
Based on the visible results, the following areas may deserve further investigation:
1. Improve on-time delivery: Review delay reasons, delivery routes, dispatch timing, and hub processing time to understand why the displayed on-time rate is 80.5%.
2. Study hub-level differences: Compare processes at Houston and Austin hubs to identify practices that may explain their displayed performance gap.
3. Investigate driver delay patterns: Review the order volumes and delay reasons for drivers with higher delay percentages before drawing conclusions about individual performance.
4. Monitor fleet availability: Review maintenance schedules and vehicle downtime because 12 of the 45 vehicles shown are marked Maintenance.
5. Reduce processing bottlenecks: Compare Hub Processing Time Hours with Delivery Time Hours to see how much of the total delivery duration occurs before dispatch.
6. Connect customer feedback to delivery outcomes: Compare satisfaction scores for delayed and on-time orders to understand whether delivery reliability is associated with customer experience.
  
## 9. Conclusion
The SwiftRoute Logistics Dashboard provides a consolidated view of logistics operations and enables users to explore delivery performance across hubs, drivers, and vehicles. By bringing operational KPIs and detailed driver analysis into one report, it helps identify performance gaps and areas that may benefit from further investigation.

**Author**: **Mohammed Uzair Dawalji**
**Project**: **SwiftRoute Logistics Dashboard**
**Platform**: **Microsoft Power BI**
