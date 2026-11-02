# SwiftRoute Logistics Dashboard

A Power BI business intelligence project for monitoring logistics operations, delivery performance, customer satisfaction, hub efficiency, driver performance, and vehicle status.

> **Project type:** Business Intelligence / Data Analytics  
> **Tool:** Microsoft Power BI  
> **Data format:** CSV  
> **Reporting period shown in the screenshots:** March–April 2024

---

## 1. Project Overview

The **SwiftRoute Logistics Dashboard** brings operational data from four datasets—Hubs, Drivers, Vehicles, and Orders—into an interactive report.

The goal is to help logistics teams answer questions such as:

- How many orders are being handled?
- What percentage of orders arrive on time?
- How satisfied are customers?
- Which hubs process the most orders, and which perform best?
- Which drivers have higher delay rates?
- What is the status of the vehicle fleet?
- How do delivery results change over time?

The report contains two pages:

1. **Logistics Overview** – a high-level view of orders, delivery KPIs, hubs, drivers, and vehicles.
2. **Drivers Overview** – a closer look at driver experience, ratings, delivery delays, and individual driver trends.

## 2. Dashboard Preview

Place the two dashboard screenshots in a folder named `screenshots` in this repository, using the filenames shown below. The image links will then display automatically on GitHub.

### Logistics Overview

![SwiftRoute Logistics Dashboard](screenshots/logistics-dashboard.png)

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

### Drivers Overview

![SwiftRoute Drivers Overview](screenshots/drivers-overview.png)

This page focuses on driver-level analysis, including:

- Driver selection
- Driver name, hire date, and years of experience
- Performance rating
- Experience versus performance rating distribution
- Drivers with the most delays
- Monthly on-time delivery trend

The report includes Year and Month filters. The Drivers Overview page also includes a driver selector and a measure selector for the trend chart.

## 3. Key Performance Indicators

The following figures are visible in the **April 2024 Logistics Overview** screenshot.

| KPI | Displayed value | What it tells us |
|---|---:|---|
| Total Orders | 1,156 | Number of orders represented by the selected dashboard context |
| On-Time Delivery Rate | 80.5% | Share of orders delivered on time |
| Customer Satisfaction (CSAT) | 84.2% | Customer satisfaction result shown by the report |
| Average Delivery Time | 35.78 hours | Average delivery duration shown by the report |

**Important:** KPI values depend on the selected Year, Month, and other report filters. They should be interpreted in the context of the filter selection, not as all-time company totals.

## 4. Dataset Description

The project uses four CSV tables. The column descriptions below explain the likely business meaning of each field based on its name and its use in the dashboard. Where a calculation or coding convention is not visible in the screenshots, it is identified as something to confirm against the source data or Power Query logic.

### 4.1 Hubs table

Contains the logistics hub master data.

| Column | Description |
|---|---|
| `Hub ID` | Unique identifier assigned to a logistics hub. |
| `HubName` | Name of the hub or logistics facility. |
| `Hub Capacity` | Hub's stated capacity. Confirm the unit and whether this means storage, order-processing, or another capacity measure. |

**How it is used:** Hub capacity is compared with order volume, and hubs are ranked by performance in the Logistics Overview page.

### 4.2 Drivers table

Contains driver information and performance attributes.

| Column | Description |
|---|---|
| `DriverID` | Unique identifier assigned to a driver. |
| `DriverName` | Driver's name. |
| `Employment Type` | Driver's employment arrangement or category, such as full-time or contract, depending on the source data. |
| `Hire Date` | Date the driver joined the organization. |
| `Experience Years` | Driver experience expressed in years. Confirm whether this is total professional experience or experience with the company. |
| `Performance Rating` | Rating assigned to the driver's performance. Confirm the scale and rating criteria in the source data. |

**How it is used:** The report compares experience with performance rating and provides a driver-level view of delivery results and delays.

### 4.3 Vehicles table

Contains vehicle details and fleet-maintenance information.

| Column | Description |
|---|---|
| `Purchase Date` | Date the vehicle was purchased. |
| `Vehicle ID` | Unique identifier assigned to a vehicle. |
| `Vehicle Model` | Vehicle's model name. |
| `Vehicle Status` | Current or recorded status of the vehicle, such as Active or Maintenance. |
| `Breakdown` | Breakdown-related field. Confirm whether this stores a count, a flag, a date, or a description. |
| `Maintenance count Alert` | Maintenance-count or alert field. Confirm its exact unit and alert logic from the source data. |
| `Vehicle Code` | Additional code used to identify or categorize a vehicle. |

**How it is used:** The dashboard summarizes vehicle status and compares order counts by vehicle model.

### 4.4 Orders table

Contains order-level delivery and operational information. This is the central transaction table for many of the report's delivery KPIs.

| Column | Description |
|---|---|
| `Order ID` | Unique identifier for an order. |
| `Actual Delivery Date` | Date the order was actually delivered. It may be blank for orders not yet delivered. |
| `Delay Reason` | Recorded reason for a delivery delay. |
| `Driver ID` | Identifier of the driver assigned to the order. |
| `Driver Name` | Name of the driver assigned to the order. |
| `Hub Name` | Hub associated with the order. |
| `Is Delayed` | Indicator showing whether the order was delayed. Confirm the stored values, such as TRUE/FALSE or 1/0. |
| `Is On Time` | Indicator showing whether the order met its on-time delivery condition. Confirm the stored values and business rule. |
| `Order Date` | Date the order was placed or created. |
| `Order Status` | Current or final order status, such as delivered, pending, or cancelled, depending on the source data. |
| `Vehicle Name` | Vehicle name or label associated with the order. Confirm how this maps to the Vehicles table. |
| `Vehicle Type` | Type or category of vehicle used for the order. |
| `Customer Satisfaction Score` | Customer satisfaction score associated with the order. Confirm the score scale and whether higher values indicate greater satisfaction. |
| `Delivery Time Hours` | Delivery duration expressed in hours. Confirm the start and end events used to calculate it. |
| `Hub Processing Time Hours` | Time spent processing the order at the hub, expressed in hours. Confirm the exact start and end events. |

**How it is used:** The Orders table supports order counts, delivery-time analysis, on-time and delayed delivery measures, customer satisfaction analysis, hub comparisons, and driver/vehicle performance analysis.

## 5. Data Model and Relationships

A sensible model for these four tables is a star-style structure, with **Orders** as the transaction table and the other tables providing descriptive attributes.

Suggested relationships to validate in Power BI:

| From table / column | To table / column | Purpose |
|---|---|---|
| `Orders[Driver ID]` | `Drivers[DriverID]` | Connect each order to its driver. |
| `Orders[Hub Name]` | `Hubs[HubName]` | Connect each order to its hub. |
| Vehicle identifier in Orders | `Vehicles[Vehicle ID]` | Connect each order to its vehicle, if a matching vehicle key exists. |

**Relationship note:** The Orders table currently lists `Vehicle Name` and `Vehicle Type`, while the Vehicles table lists `Vehicle ID`, `Vehicle Model`, and `Vehicle Code`. These fields are not necessarily equivalent. Confirm the actual key mapping before creating a vehicle relationship. If no reliable matching key exists, avoid creating a relationship based only on similar-looking labels.

For a robust model, use unique IDs as relationship keys wherever possible. Check that the lookup-side key is unique and that data types match on both sides.

## 6. Dashboard Walkthrough

### Page 1 – Logistics Overview

| Visual / section | Business question it helps answer |
|---|---|
| KPI cards | What is the current order volume and overall delivery performance? |
| Hub capacity and total orders | How does order volume compare across hubs and their stated capacity? |
| Hub performance ranking | Which hubs have the strongest and weakest displayed performance percentages? |
| Experience vs Rating scatter chart | How are driver experience and performance ratings distributed? |
| Drivers with most delays | Which drivers have the highest displayed delay percentages? |
| Vehicle status doughnut chart | How many vehicles are active versus in maintenance? |
| Orders by vehicle model | Which vehicle models are associated with the most orders? |

### Page 2 – Drivers Overview

| Visual / section | Business question it helps answer |
|---|---|
| Driver selector | Which individual driver's information should be inspected? |
| Driver information card | What are the selected driver's hire date, experience, and rating? |
| Experience vs Rating scatter chart | How does the selected driver population's experience relate to performance ratings? |
| Drivers with most delays | Which drivers have the highest displayed delay percentages? |
| Monthly trend chart | How does the selected delivery measure change month by month? |

## 7. Findings Visible in the Screenshots

The following are observations from the supplied dashboard screenshots. They are not claims about the full dataset beyond the filter context shown.

### 7.1 Overall logistics findings – April 2024

- The dashboard displays **1,156 total orders**.
- The displayed on-time delivery rate is **80.5%**. This suggests that roughly one in five orders did not meet the on-time condition, subject to the report's measure definition.
- The displayed customer satisfaction score is **84.2%**.
- Average delivery time is **35.78 hours**.
- The overview shows **6 hubs**, **55 drivers**, and **45 vehicles**.

### 7.2 Hub performance – April 2024

The Hub Performance Ranking visual shows the following percentages:

| Hub | Displayed performance |
|---|---:|
| Houston Hub | 82.6% |
| Dallas Main Hub | 80.9% |
| El Paso Hub | 80.5% |
| San Antonio Hub | 79.8% |
| Fort Worth Hub | 79.3% |
| Austin Hub | 78.1% |

- Houston Hub has the highest displayed performance at **82.6%**.
- Austin Hub has the lowest displayed performance at **78.1%** among the six hubs shown.
- The difference between the highest and lowest displayed hub performance is **4.5 percentage points**.

These values are the percentages displayed in the ranking visual. Confirm the underlying measure definition before interpreting them as an on-time rate or another specific KPI.

### 7.3 Vehicle status – April 2024

The vehicle status visual shows:

- **45 vehicles** in total.
- **33 Active vehicles (73.33%)**.
- **12 Maintenance vehicles (26.67%)**.

This indicates that just under three-quarters of the displayed fleet is marked Active, while a little over one-quarter is marked Maintenance.

### 7.4 Driver delay findings – April 2024

The visible Drivers with most Delays chart lists:

| Driver | Displayed delay percentage |
|---|---:|
| Matthew Smith | 42.1% |
| Kevin Jones | 41.2% |
| Charles Lopez | 40.0% |
| Donald Jackson | 33.3% |
| Jennifer White | 30.3% |
| John Smith | 28.6% |
| Patricia Jones | 28.6% |
| Matthew Williams | 28.0% |
| Daniel Brown | 27.6% |
| Charles Hernandez | 26.7% |

Matthew Smith has the highest displayed delay percentage in this chart. These percentages should be reviewed alongside each driver's order count: a percentage based on a small number of orders can be less stable than one based on a larger sample.

### 7.5 Individual driver view – March 2024

The Drivers Overview screenshot is filtered to **March 2024** and shows **Barbara Clark** selected.

- The selected-driver card states that Barbara Clark made **18 deliveries** in March 2024.
- The card displays a hire date of **07/08/2021** and **5 years** of experience.
- The monthly trend visual shows the selected delivery measure changing across the year, with the highest visible point at **88% in August** and the lowest at **69% in November**.

The trend chart's measure selector is set to **On Time Delivery Rate** in the screenshot. Because the page is filtered to March while the chart displays January–December, confirm the exact interaction and filter behavior in the PBIX before treating the line as a March-only trend.

### 7.6 Interpretation and business opportunities

Based on the visible results, the following areas may deserve further investigation:

1. **Improve on-time delivery:** Review delay reasons, delivery routes, dispatch timing, and hub processing time to understand why the displayed on-time rate is 80.5%.
2. **Study hub-level differences:** Compare processes at Houston and Austin hubs to identify practices that may explain their displayed performance gap.
3. **Investigate driver delay patterns:** Review the order volumes and delay reasons for drivers with higher delay percentages before drawing conclusions about individual performance.
4. **Monitor fleet availability:** Review maintenance schedules and vehicle downtime because 12 of the 45 vehicles shown are marked Maintenance.
5. **Reduce processing bottlenecks:** Compare `Hub Processing Time Hours` with `Delivery Time Hours` to see how much of the total delivery duration occurs before dispatch.
6. **Connect customer feedback to delivery outcomes:** Compare satisfaction scores for delayed and on-time orders to understand whether delivery reliability is associated with customer experience.

These are investigation opportunities, not proven causes. The dataset and measure definitions should be checked before making operational decisions.

## 8. Suggested Further Analysis

The existing report could be extended with:

- Delay reasons by frequency and percentage.
- On-time delivery rate by hub, driver, and vehicle type.
- Average hub processing time by hub.
- Customer satisfaction for delayed versus on-time orders.
- Delivery-time trends by month.
- Vehicle breakdown and maintenance analysis.
- Driver performance by employment type and experience band.
- Order status distribution, including pending and cancelled orders.

## 9. How to Use This Project

1. Clone or download this repository.
2. Open the `.pbix` file in Microsoft Power BI Desktop.
3. If Power BI requests the source files, update the data-source paths to the CSV files included in the repository.
4. Select **Refresh** to load the data.
5. Use the Year and Month filters to explore different reporting periods.
6. Navigate between Logistics Overview and Drivers Overview.
7. On the Drivers Overview page, select a driver and a measure to inspect the individual view and trend.

> The exact refresh steps may vary depending on how the original PBIX file connects to the CSV files.

## 10. Repository Structure

A suggested GitHub repository layout:

```text
SwiftRoute-Logistics-Dashboard/
│
├── README.md
├── SwiftRoute_Logistics_Dashboard.pbix
│
├── data/
│   ├── Hubs.csv
│   ├── Drivers.csv
│   ├── Vehicles.csv
│   └── Orders.csv
│
└── screenshots/
    ├── logistics-dashboard.png
    └── drivers-overview.png
```

Only include data that you are permitted to share. If the CSV files contain personal, confidential, or commercially sensitive information, use anonymized or sample data instead.

## 11. Skills Demonstrated

- Power BI dashboard development
- Data modelling and table relationships
- Data cleaning and transformation with Power Query
- KPI design and business performance reporting
- DAX measures (where used in the report)
- Interactive filters and drill-down analysis
- Logistics and operations analytics
- Data storytelling and business insight communication

## 12. Conclusion

The SwiftRoute Logistics Dashboard provides a consolidated view of logistics operations and enables users to explore delivery performance across hubs, drivers, and vehicles. By bringing operational KPIs and detailed driver analysis into one report, it helps identify performance gaps and areas that may benefit from further investigation.

---

**Author:** Mohammed Uzair Dawalji  
**Project:** SwiftRoute Logistics Dashboard  
**Platform:** Microsoft Power BI

