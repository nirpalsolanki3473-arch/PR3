# E-Commerce Sales Dashboard — Power BI

An interactive Power BI dashboard analyzing online retail performance: sales trends, geographic distribution, payments, and customer reviews. Built as a single `.pbix` file with three report pages on top of an order-fulfillment star-schema data model (order items, customers, sellers, payments, and reviews).

> 📸 **Dashboard previews:** _add screenshots here once exported (see [Screenshots](#screenshots) section below)._

---

## 📊 Overview

This dashboard helps e-commerce/operations teams answer questions like:

- How is revenue and order volume trending month over month?
- Which product categories sell the most, and how are they rated?
- Where are our sellers and customers geographically concentrated?
- How do customers prefer to pay, and how does payment value relate to satisfaction?

It supports filtering by **Year**, **Order Status**, **Product Category**, and **Payment Value Range**, so you can drill from company-wide totals down to a specific category, region, or payment segment.

---

## 🗂️ Report Pages

### 1. Sales Overview
The executive summary page — top-line KPIs and sales trends.

| Visual | Type | Purpose |
|---|---|---|
| Total Orders | Card | Order volume |
| Total Revenue | Card | Sum of order item prices |
| Avg Order Value | Card | Average revenue per order |
| Avg Customer Rating | Card | Average review score |
| Top 10 Categories Bar Chart | Clustered Bar Chart | Best-selling product categories |
| Monthly Order Trend | Line Chart | Order volume over time |

**Filters:** Year, Order Status, Product Category

### 2. Geographic Analysis
Where the sales and fulfillment activity is happening.

| Visual | Type | Purpose |
|---|---|---|
| Revenue by Seller State | Map | Geographic revenue distribution |
| Top 10 Seller Cities by Revenue | Clustered Bar Chart | City-level revenue ranking |
| Highest Revenue Seller States | Clustered Column Chart | State-level revenue ranking |

**Filters:** Year

### 3. Payments & Reviews
Payment behavior and customer satisfaction.

| Visual | Type | Purpose |
|---|---|---|
| Revenue by Payment Type | Donut Chart | Payment method mix |
| Average Review Score of 10 Selling Categories | Clustered Bar Chart | Satisfaction by category |
| Detail pivot table | Pivot Table | Row-level payment/review breakdown |

**Filters:** Year, Payment Value Range

---

## 🧮 Data Model

The model follows a **star schema** typical of an order-fulfillment dataset, with one central order-items fact table joined to customer, seller, product, payment, review, and date dimensions.

```
FactOrderItems (central fact table)
   ├── Dimorders      (order-level attributes: status, dates)
   ├── DimCustomer    (customer details, state)
   ├── Dimsellers     (seller details, state, city)
   ├── DimProducts    (product category)
   ├── FactPayments   (payment type, value)
   ├── FactReviews    (review score)
   └── Dimdate        (date dimension: Year, etc.)
```

| Table | Role |
|---|---|
| `FactOrderItems` | Core fact table — order line items, price |
| `Dimorders` | Order metadata — order ID, status |
| `DimCustomer` | Customer details — state |
| `Dimsellers` | Seller details — state, city |
| `DimProducts` | Product category (English-translated) |
| `FactPayments` | Payment type, payment value, payment value category |
| `FactReviews` | Customer review scores |
| `Dimdate` | Date dimension for time intelligence (Year) |

### Key Measures / Aggregations
- `Total Orders` — distinct/total count of orders
- `Total Revenue` — `SUM(price)` from `FactOrderItems`
- `Avg_Order_Value` — average revenue per order
- `Avg Review Score` — average of `review_score`

### Key Columns
- `order_id`, `order_status`, `price`
- `customer_state`, `seller_state`, `seller_city`
- `Product_Category_EN`
- `payment_type`, `payment_value`, `Payment_Value_Category`
- `review_score`
- `Year`

---

## 🛠️ Tech Stack

- **Tool:** Microsoft Power BI Desktop
- **Data modeling:** Star schema (fact + dimension tables)
- **Visuals:** Cards, bar/column charts, line chart, donut chart, map, pivot table, slicers, dynamic page navigation

---

## 🚀 How to Use

1. Download `pr3.pbix` from this repo.
2. Open it in [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free).
3. Use the slicers (Year, Order Status, Product Category, Payment Value Range) to filter the view.
4. Navigate between **Sales Overview → Geographic Analysis → Payments & Reviews** using the in-report page navigator.

> **Note:** This file connects to a fixed/embedded dataset, so visuals will render as-is. To use it with your own data, update the underlying tables in Power BI's data model.

---

## 📁 Repo Structure

```
├── pr3.pbix          # Power BI report file
├── README.md         # This file
└── screenshots/      # Dashboard images (add yours here)
```

---

## 📸 Screenshots

_Add your dashboard screenshots below once exported from Power BI (File → Export → PDF/Image, or simple screen capture of each page):_

### Sales Overview Page
![Project Screenshot](<Screenshot 2026-06-11 160500.png>)

### Geographic Analysis Page
![Project Screenshot](<Screenshot 2026-06-10 184502.png>)

### Payments & Reviews Page
![Project Screenshot](<Screenshot 2026-06-10 184550.png>)

## Relationship Diagram
![Relation Diagram](<Screenshot 2026-06-11 162544.png>)

## DAX Formulas
[Order Date Formula](<(1)Order_Date =.txt>)

---

## 📌 Future Improvements

- [ ] Add drill-through pages for individual seller/customer detail
- [ ] Add YoY revenue and order volume comparisons
- [ ] Connect to a live data source instead of static data
- [ ] Add delivery time / logistics analysis page

---

## 📄 License

Add a license of your choice (e.g., MIT) if you want others to reuse this report template.
