# PowerBI-Superstore-Analytics

<img width="1015" height="568" alt="image" src="https://github.com/user-attachments/assets/2005416b-3347-478c-82cb-cbcd442be638" />


# Global Superstore - Executive Sales & Profitability Analytics

An interactive Power BI Executive Dashboard built on the Kaggle Global Superstore dataset (51,000+ transactional records). The project analyzes global revenue velocity, profit margin health, product profitability, and root-cause drivers across multi-tier regional markets.

---

## Architecture & Data Modeling

The solution utilizes a **Star Schema** architecture to enable time-intelligence calculations without compromising query performance:

```text
[ Dim_Date (Calendar Dimension) ]
              │ (1)
              │
              ▼ (*)
     [ Fact_Orders (51k+ Records) ]

Power Query ETL: Handled date-time formatting, cleaned corrupted character encodings, removed unindexed artifacts, and optimized column types.

Date Dimension (Dim_Date): Custom calendar generated using DAX covering contiguous fiscal periods from 2011 to 2014, with month names indexed against strict month numbers.

Data Modeling: 1-to-Many single-directional relationship between Dim_Date[Date] and Orders[Order.Date].

DAX Measures Implemented
All calculations are encapsulated inside an independent _Measures table:

Total Revenue:
Total Sales = SUM(Orders[Sales])

Total Profit:
Total Profit = SUM(Orders[Profit])

Operating Profit Margin (%):
Profit Margin % = DIVIDE([Total Profit], [Total Sales], 0)

Order Velocity:
Total Orders = DISTINCTCOUNT(Orders[Order.ID])

Year-over-Year (YoY) Sales Comparison:
Sales LY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR(Dim_Date[Date]))
YoY Sales Growth % = DIVIDE([Total Sales] - [Sales LY], [Sales LY], 0)

Dashboard Visuals Breakdown
Executive KPI Cards: Immediate visibility into top-line indicators:
Total Sales: ₹12.64M
Total Profit: ₹1.47M
Profit Margin: 11.61%
Total Orders: 25K

Monthly Trend Analysis (Line Chart): Multi-line tracking of Sales vs. Profit from January through December.

Product Profitability Analysis (Clustered Bar Chart): Identifies top revenue drivers (Copiers, Phones) versus underperforming sub-categories.

AI Root-Cause Decomposition Tree: Dynamic breakdown analyzing how profit trickles down from Category $\rightarrow$ Sub-Category $\rightarrow$ Region $\rightarrow$ Shipping Mode.

Interactive Slicers: Global cross-filtering by Year (2011–2014), Market Region, and Customer Segment (Consumer, Corporate, Home Office).

Dashboard PreviewHow to View and RunClone or download this repository.Ensure Power BI Desktop is installed.Open Global_Superstore_Executive_Dashboard.pbix.Refresh dataset if re-pointing to a local superstore.csv path.
