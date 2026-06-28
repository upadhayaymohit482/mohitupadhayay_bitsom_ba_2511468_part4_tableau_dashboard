# Part 4: Tableau Executive Dashboard — Retail Sales Performance

## Business Problem Summary

The retail leadership team requires a comprehensive executive dashboard to monitor and analyze sales performance, profitability, customer segment behavior, category performance, shipping efficiency, discount impact, and return patterns. The goal is to enable data-driven decision-making by identifying key business opportunities and risks across a two-year period (2024–2025).

---

## Dataset Description

**File:** `data/dashboard_sales_data.xlsx`
**Sheet:** `dashboard_sales_data`
**Records:** 4,200 orders
**Date Range:** January 1, 2024 – December 31, 2025

### Fields and Data Types

| Field | Type | Description |
|---|---|---|
| order_id | String | Unique order identifier |
| order_date | Date | Date the order was placed |
| ship_date | Date | Date the order was shipped |
| customer_id | String | Unique customer identifier |
| customer_segment | String (Categorical) | Consumer, Corporate, Home Office |
| region | String (Categorical) | North, South, East, West |
| state | String (Geographic) | 19 Indian states |
| city | String (Geographic) | City within state |
| category | String (Categorical) | Furniture, Office Supplies, Technology |
| sub_category | String (Categorical) | 14 sub-categories |
| product_name | String | Individual product name |
| ship_mode | String (Categorical) | Same Day, First Class, Second Class, Standard Class |
| sales | Decimal | Order revenue in INR |
| quantity | Integer | Units ordered |
| discount | Decimal | Discount percentage (0.0–0.35) |
| profit | Decimal | Order profit in INR (can be negative) |
| return_flag | Binary (0/1) | 1 = returned, 0 = not returned |
| delivery_days | Integer | Days from order to ship |
| customer_rating | Decimal | Customer satisfaction rating (1.0–5.0) |
| campaign_channel | String (Categorical) | Organic, Social, Paid, Email, Referral (some nulls) |

---

## Tableau Workbook Description

**File:** `tableau/executive_dashboard.twbx`

The packaged workbook contains the following sheets and one master dashboard:

### Sheets Included

| Sheet Name | Purpose |
|---|---|
| Sales Trend View | Monthly sales and profit line chart over 2024–2025 |
| Regional Performance View | Map + bar chart of sales/profit by state and region |
| Category Profitability View | Sub-category profit bar chart with diverging color |
| Customer Segment View | Grouped bar chart comparing segments on sales and profit |
| Shipping Performance View | Bar chart + table of ship mode efficiency and profitability |
| Discount vs Profit View | Scatter plot of discount vs. profit per order |
| Return Analysis View | Return rate bar chart by category and segment |

### Dashboard
**Executive Dashboard** — combines all seven views with KPI cards and interactive filters.

---

## Calculated Fields Created

| Field Name | Formula | Purpose |
|---|---|---|
| Profit Margin | `SUM([Profit]) / SUM([Sales])` | Profitability as % of revenue |
| Cost | `SUM([Sales]) - SUM([Profit])` | Derived cost of goods sold |
| Average Order Value | `SUM([Sales]) / COUNTD([Order Id])` | Revenue per unique order |
| Return Rate | `SUM([Return Flag]) / COUNT([Order Id])` | Proportion of returned orders |
| Shipping Delay Bucket | IF/ELSEIF on Delivery Days | Categorizes delivery speed into 5 buckets |

---

## Dashboard Components

### KPI Cards (Summary Metrics)
1. **Total Sales** — SUM(Sales) formatted in INR millions
2. **Total Profit** — SUM(Profit) formatted in INR millions
3. **Overall Profit Margin** — Profit Margin calculated field, formatted as %
4. **Average Order Value** — Average Order Value calculated field
5. **Overall Return Rate** — Return Rate calculated field, formatted as %

### Charts / Views (7 total)
1. Sales Trend (Line Chart)
2. Regional Performance (Map + Bar)
3. Category Profitability (Sorted Bar with diverging color)
4. Customer Segment (Grouped Bar)
5. Shipping Performance (Bar + Highlight Table)
6. Discount vs Profit (Scatter Plot)
7. Return Analysis (Bar Chart)

---

## Filters and Interactions Used

### Interactive Filters Applied to Dashboard
1. **Region** — Filter to North, South, East, West
2. **Category** — Filter to Furniture, Office Supplies, Technology
3. **Customer Segment** — Filter to Consumer, Corporate, Home Office
4. **Order Date Range** — Date range filter (year/quarter/month)
5. **Ship Mode** — Filter to Same Day, First Class, Second Class, Standard Class
6. **Campaign Channel** — Filter to Organic, Social, Paid, Email, Referral

### Actions / Interactions
- **Filter Action:** Clicking a region on the map filters all other charts on the dashboard to that region
- **Highlight Action:** Hovering over a category in the profitability chart highlights matching bars in the segment chart
- **Tooltip:** All charts include rich tooltips showing additional context on hover

---

## Key Business Insights

1. **Technology drives 71% of revenue** with an 18.2% profit margin — the highest of all categories.
2. **South region leads** with ₹64.7M in sales and the highest absolute profit.
3. **Furniture margins are thin** (6.9%) due to heavy discounting, with Tables and Bookcases near breakeven.
4. **30–35% discount tier produces net losses** (cumulative -₹102K) — a discount governance policy is urgently needed.
5. **Home Office is the most profitable segment** (15.5% margin) and deserves targeted Technology campaigns.
6. **Furniture return rate of 7.67%** is more than double the Technology rate — quality or expectation issues are likely.
7. **Mid-year dips in April–May and August** are predictable and addressable through seasonal promotional planning.
8. **Standard Class delivery averages 4.71 days** — a potential customer satisfaction risk in a market with rising delivery expectations.

---

## Dashboard Story Summary

The business is performing well overall (₹217M revenue, 15.3% margin), led by Technology and the South region. However, two structural risks demand immediate attention: loss-making Furniture orders at high discounts, and a high Furniture return rate. The recommended actions are: enforce a discount cap policy, investigate Furniture return root causes, and invest in Technology penetration in underperforming regions (West, East). Seasonal revenue recovery campaigns in Q2 represent a near-term opportunity to smooth annual performance.

---

## Assumptions and Limitations

### Assumptions
- `delivery_days` represents the number of days from order_date to ship_date (not delivery_date). Actual delivery to customer may be longer.
- `return_flag = 1` means the order was returned; no partial returns are modeled.
- `profit` is net profit after discount but before returns processing cost.
- `campaign_channel` nulls (~3–5% of records) are treated as "Unknown" and excluded from channel analysis.
- Dates stored as Excel serial numbers were correctly parsed to date format in Tableau.

### Limitations
- No customer-level analysis possible (no repeat purchase frequency or CLV data).
- Return reason codes are not available — root-cause analysis of returns requires additional data.
- No external market benchmark data — regional comparisons are internal only.
- City-level geographic granularity was not used in the dashboard due to the large number of cities (maps would be too dense).

---

## Screenshots Included

| File | Contents |
|---|---|
| `screenshots/full_dashboard.png` | Complete executive dashboard with all KPIs and charts |
| `screenshots/sales_trend_view.png` | Monthly sales and profit trend line chart (2024–2025) |
| `screenshots/regional_performance_view.png` | State-level map and regional bar chart |
| `screenshots/category_profitability_view.png` | Sub-category profitability bar chart with diverging colors |
| `screenshots/filter_interaction_view.png` | Dashboard with Region and Category filters applied |
