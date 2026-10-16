# 🌮 TacoGo Delivery – Performance Dashboard Project

## 📌 Project Overview
TacoGo is a multi-city taco delivery business looking to gain clear visibility into operational performance, delivery times, order volumes, and menu popularity across regions. 

This project delivers a single-page interactive **Power BI Dashboard** engineered on top of a relational **Star Schema Data Model** with dynamic **DAX time-intelligence** filtering.

---

## 📊 Executive KPI Summary
* **Total Orders:** 1,000
* **Total Revenue:** $6,908.25
* **Total Tips Collected:** $1,806.11
* **Average Delivery Duration:** 50.93 minutes
* **Average Delivery Distance:** 13.07 km

---

## 🏗️ Data Architecture & Star Schema Model

The data model follows standard dimensional modeling principles, organizing flat order logs into a single **Fact Table** surrounded by three **Dimension Tables**:

* **`FactOrders`**: Records individual transactional data (Price, Tip, Distance, Delivery Duration, Order Date, Restaurant ID, Taco ID).
* **`DimRestaurant`**: Contains lookup information on restaurant names and location cities.
* **`DimTaco`**: Details taco menu items, size classifications (*Large*, *Regular*), and taco types.
* **`DimDate`**: Dynamic DAX calendar table generated from order date boundaries (`2024-01-01` to `2025-12-02`), marked as an official Date Table.

### Model Relationships:
* `DimDate[Date]` $1 \rightarrow *$ `FactOrders[Order Date]`
* `DimRestaurant[Restaurant ID]` $1 \rightarrow *$ `FactOrders[Restaurant ID]`
* `DimTaco[Taco ID]` $1 \rightarrow *$ `FactOrders[Taco ID]`

---

## 📑 Dashboard Layout & Visual Features

1. **Executive KPI Cards Banner:** Top-level metrics for revenue, order volume, tip collection, delivery speed, and distance.
2. **Orders Trend by Month (Line Chart):** Tracks monthly order fluctuations over time.
3. **Top Restaurants by Order Volume (Horizontal Bar Chart):** Compares demand across individual restaurant locations.
4. **Taco Type Distribution (Donut Chart):** Visualizes order proportions across menu choices (*Chicken, Fish, Veggie, Pork, Beef*).
5. **Revenue by Taco Size & Type (Stacked Column Chart):** Breaks down revenue contributions across sizes (*Large* vs *Regular*) segmented by taco flavor.
6. **Year Slicer:** Enables dynamic temporal filtering across all visuals for 2024 and 2025.

---

## 🧮 DAX Measures Implemented

```dax
Total Orders = COUNTROWS('FactOrders')

Total Revenue = SUM('FactOrders'[Price ($)])

Avg Delivery Duration = AVERAGE('FactOrders'[Delivery Duration (min)])

Avg Distance = AVERAGE('FactOrders'[Distance (km)])

Total Tips = SUM('FactOrders'[Tip ($)])
