# ☕ Coffee Shop Sales Analysis Dashboard

An interactive **Power BI** dashboard that analyzes sales data for a local coffee shop chain. It tracks core KPIs, breaks performance down by product, store location and time, and helps stakeholders spot sales patterns, identify top-performing products and optimize operations.

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Business Objectives](#-business-objectives)
- [Dataset](#-dataset)
- [Key Metrics (KPIs)](#-key-metrics-kpis)
- [DAX Measures](#-dax-measures)
- [Dashboard Features](#-dashboard-features)
- [Tools & Technologies](#-tools--technologies)
- [Repository Structure](#-repository-structure)
- [Key Insights](#-key-insights)
- [Author](#-author)

---

## 📖 Project Overview

The **Coffee Shop Sales Analysis Dashboard** visualizes transactional sales data and turns it into actionable insights. It focuses on:

- Total sales, total orders and total quantity sold
- Month-over-month (MoM) comparison of performance
- Sales breakdown by **product category**, **product type** and **store location**
- Sales trends across days, weeks and months

## 🎯 Business Objectives

- Monitor overall sales performance at a glance
- Identify best- and worst-performing products and categories
- Compare performance across store locations
- Understand time-based trends (daily, weekly, monthly, peak hours)
- Support data-driven decisions on inventory, staffing and promotions

---

## 🗂 Dataset

Each row represents a single transaction line.

| Column | Description |
|---|---|
| `transaction_id` | Unique identifier for each transaction |
| `transaction_date` | Date of the transaction |
| `transaction_time` | Time of the transaction |
| `transaction_qty` | Quantity of items sold in the transaction |
| `store_id` | Unique identifier for the store |
| `store_location` | Location of the store |
| `product_id` | Unique identifier for the product |
| `unit_price` | Price per unit of the product |
| `product_category` | Category of the product |
| `product_type` | Type of product within the category |
| `product_detail` | Specific details of the product |

> **Calculated column:** `Sales = transaction_qty × unit_price`

---

## 📊 Key Metrics (KPIs)

| KPI | Description |
|---|---|
| **Total Sales** | Sum of sales revenue for the selected period |
| **Total Orders** | Number of distinct orders placed |
| **Total Quantity Sold** | Total number of units sold |
| **Average Sales** | Average daily sales amount |
| **Previous Month Sales / Orders / Qty** | Values for the previous month, used for MoM comparison |
| **Current Month Sales** | Month-to-date sales for the selected month |

---

## 🧮 DAX Measures

### Total Sales
```DAX
Total Sales = SUM(Transactions[Sales])
```

### Total Orders
```DAX
Total Orders = DISTINCTCOUNT(Transactions[transaction_id])
```

### Total Quantity Sold
```DAX
Total Quantity Sold = SUM(Transactions[Transaction_Qty])
```

### Average Sales (Daily)
```DAX
Average Sales =
AVERAGEX(
    ALLSELECTED(Transactions[transaction_date]),
    'Date Table'[Total Sales]
)
```

### Current Month Sales (CM)
```DAX
CM =
VAR selected_month = SELECTEDVALUE('Date Table'[Month])
RETURN
    TOTALMTD(
        CALCULATE(
            SUM(Transactions[Sales]),
            'Date Table'[Month] = selected_month
        ),
        'Date Table'[Date]
    )
```

### Previous Month Sales
```DAX
Previous Month Sales =
CALCULATE(
    'Transactions'[CM],
    DATEADD('Date Table'[Date], -1, MONTH)
)
```

### Previous Month Orders
```DAX
Previous Month Orders =
CALCULATE(
    'Transactions'[CM Orders],
    DATEADD('Date Table'[Date], -1, MONTH)
)
```

### Previous Month Quantity Sold
```DAX
Previous Month Quantity Sold =
CALCULATE(
    'Transactions'[CM Qty],
    DATEADD('Date Table'[Date], -1, MONTH)
)
```

> **Note:** `CM Orders` and `CM Qty` follow the same pattern as `CM`, using `DISTINCTCOUNT(transaction_id)` and `SUM(transaction_qty)` respectively.

---

## 🖥 Dashboard Features

- **KPI cards** with month-over-month comparison
- **Sales trend** over time (daily / monthly)
- **Sales by product category** and **product type**
- **Sales by store location**
- **Top products** by revenue and quantity
- **Interactive slicers** for month, store location and product category
- **Cross-filtering** between visuals

---

## 🛠 Tools & Technologies

- **Power BI Desktop** (data modeling, visualization)
- **DAX** (measures and time intelligence)
- **Power Query** (data cleaning and transformation)
- **Excel / CSV** (data source)

> Adjust file and folder names to match your actual repository.

---

## 💡 Key Insights

- Coffee is the product category that contributes maximum share in the reveneu that is **$269.95k**.
- Hells's Kitchen lead with **$236.51k** in sales and total of **50735** order in 
- Peak sales hours ia at **10 AM** and days of the week are on **Weekdays**
- Best-selling product types is **Barista Espresso** and underperformers is **Green Beans**

---

## 👤 Author

**Sumit**
Aspiring Data Analyst | SQL • Python • Power BI • Tableau • Excel


⭐ If you found this project useful, consider giving the repo a star!
