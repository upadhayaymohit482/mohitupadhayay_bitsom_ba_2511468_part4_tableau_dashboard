# Business Insights — Executive Dashboard
## Retail Leadership Team | Sales Performance Analysis (2024–2025)

---

## Calculated Fields Explanation

| Calculated Field | Formula (Tableau Syntax) | Purpose |
|---|---|---|
| **Profit Margin** | `SUM([Profit]) / SUM([Sales])` | Measures profitability as a percentage of revenue; essential for identifying low-margin categories or regions |
| **Cost** | `SUM([Sales]) - SUM([Profit])` | Derives total cost of goods sold; useful for cost benchmarking |
| **Average Order Value** | `SUM([Sales]) / COUNTD([Order Id])` | Calculates revenue per unique order; helps understand customer purchasing behavior |
| **Return Rate** | `SUM([Return Flag]) / COUNT([Order Id])` | Percentage of orders returned; indicates product quality or customer satisfaction issues |
| **Shipping Delay Bucket** | `IF [Delivery Days] = 0 THEN "Same Day" ELSEIF [Delivery Days] <= 2 THEN "Fast (1-2 days)" ELSEIF [Delivery Days] <= 4 THEN "Standard (3-4 days)" ELSEIF [Delivery Days] <= 6 THEN "Slow (5-6 days)" ELSE "Very Slow (7+ days)" END` | Categorizes delivery speed for operational analysis |

---

## Business Insights

### 1. Sales Trend Insight — Mid-Year Dip is a Recurring Pattern

**Observation:** Sales consistently dip in April–May and July–August across both 2024 and 2025, while January, September, and October–November show strong peaks.

**Data Evidence:** April 2025 recorded ₹7.19M in sales — one of the lowest months. August 2024 was the weakest at ₹6.30M. July 2025 rebounded to ₹10.66M (the highest single month).

**Business Interpretation:** The pattern suggests demand seasonality. The mid-year slowdown may reflect budget cycles for corporate and government buyers.

**Recommended Action:** Launch targeted promotions in April–May to stimulate demand during the predictable slow period. Consider bundled offers for Corporate segment during these months.

---

### 2. Regional Performance — South Region Leads, West Lags on Margin

**Observation:** The South region is the top performer in both sales and profit, while the West region has the lowest profit despite comparable sales volume.

**Data Evidence:** South: ₹64.7M sales, ₹9.99M profit (margin ~15.4%). West: ₹48.9M sales, ₹7.4M profit (margin ~15.1%). North: ₹54.6M sales, ₹8.3M profit.

**Business Interpretation:** South region — driven by Hyderabad, Bengaluru, and Chennai — benefits from stronger Technology demand. West region's lower margin likely reflects higher discount usage or less favorable product mix.

**Recommended Action:** Replicate the South region's product mix and sales approach in the West. Conduct a discount audit for West region to identify margin leakage.

---

### 3. Category Profitability — Technology is the Profit Engine

**Observation:** Technology accounts for 71% of total revenue and delivers an 18.2% profit margin. Furniture generates 24% of revenue but only a 6.9% margin.

**Data Evidence:** Technology: ₹153.9M sales, ₹28.0M profit (18.2% margin). Furniture: ₹51.6M sales, ₹3.6M profit (6.9% margin). Office Supplies: ₹11.5M sales, ₹1.7M profit (14.85% margin).

**Business Interpretation:** Furniture's thin margin is driven by high discount rates and loss-making sub-categories (Tables, Bookcases). Technology's margin is anchored by Copiers and Accessories.

**Recommended Action:** Re-evaluate the pricing and discount policy for Furniture. Invest more in Technology cross-selling.

---

### 4. Sub-Category Risk — Tables and Bookcases are Loss Risks at High Discounts

**Observation:** Within Furniture, Tables and Bookcases show near-zero or negative profit at 30%+ discount levels.

**Data Evidence:** Tables: ₹12.9M sales, ₹731K profit (~5.7% margin). Bookcases: ₹12.5M sales, ₹711K profit (~5.7% margin). Individual orders show negative profit at 30–35% discount.

**Business Interpretation:** Excessive discounting on large Furniture items turns orders loss-making. These products may be used to win bids without adequate margin protection.

**Recommended Action:** Set a minimum discount floor of 20% for Tables and Bookcases. Flag any orders exceeding this limit for manager approval before processing.

---

### 5. Customer Segment — Home Office is the Most Profitable Segment

**Observation:** The Home Office segment has the highest total sales and profit, though all three segments perform within a narrow margin band.

**Data Evidence:** Home Office: ₹74.5M sales, ₹11.6M profit (~15.5% margin). Consumer: ₹71.9M, ₹11.0M (~15.3%). Corporate: ₹70.6M, ₹10.7M (~15.2%).

**Business Interpretation:** Home Office buyers tend to purchase higher-value Technology products with less negotiated discounting, giving a slight margin edge.

**Recommended Action:** Design targeted campaigns for Home Office segment focused on Technology bundles. For Corporate clients, implement volume-based loyalty incentives to grow average order value.

---

### 6. Discount Impact — Heavy Discounts Are Destroying Profit

**Observation:** Orders at 30–35% discount collectively produce a net loss. Orders with discounts under 10% are by far the most profitable.

**Data Evidence:** 0–10% discount: ₹123.4M sales, ₹23.3M profit (18.9% margin). 30–35% discount: ₹2.07M sales, -₹102K profit (negative margin).

**Business Interpretation:** The company is making loss-making sales at the highest discount tier — a direct margin leakage issue driven by undisciplined field discounting.

**Recommended Action:** Enforce a discount cap policy. Remove or restrict the 30–35% discount tier. Implement a discount impact calculator for the sales team to visualize profit impact before applying discounts.

---

### 7. Shipping Performance — Same Day Adds Value Despite Lower Volume

**Observation:** Standard Class dominates volume (highest sales) but has the slowest average delivery at 4.71 days. Same Day delivery achieves 0.4-day average with healthy margins.

**Data Evidence:** Standard Class: ₹122.8M sales, ₹19.1M profit, avg 4.71 days. Same Day: ₹14.6M sales, ₹2.19M profit, avg 0.4 days. First Class: ₹31.9M sales, avg 1.77 days.

**Business Interpretation:** Premium shipping options (First Class, Same Day) maintain profitability while improving customer experience. Standard Class slow delivery may be contributing to lower satisfaction scores.

**Recommended Action:** Promote First Class for Technology orders. Consider Same Day as a premium paid upgrade to grow this profitable segment without cannibalizing Standard Class margins.

---

### 8. Return Pattern — Furniture Return Rate of 7.7% is a Major Risk

**Observation:** Furniture has the highest return rate at 7.67%, more than double the Technology return rate of 3.03%.

**Data Evidence:** Furniture return rate: 7.67%. Office Supplies: 3.65%. Technology: 3.03%. Overall portfolio return rate: 4.55%.

**Business Interpretation:** The high Furniture return rate points to quality issues, misaligned customer expectations (online product imagery), or delivery damage. Each return represents a revenue reversal plus an additional logistics cost.

**Recommended Action:** Investigate root causes by sub-category (Chairs, Tables, Bookcases). Improve product descriptions, packaging standards, and implement post-delivery quality checks for Furniture orders.

---

## Summary of Risks and Opportunities

| Area | Risk / Opportunity | Priority |
|---|---|---|
| Technology margins (18.2%) | Strong profit engine — grow further | High Opportunity |
| Furniture at 30–35% discount | Net loss-making — direct margin leakage | High Risk |
| South region performance | Top performer — replicate strategies elsewhere | Opportunity |
| Furniture return rate (7.7%) | Erodes margin and adds logistics cost | High Risk |
| Mid-year seasonal dip (Apr–May) | Predictable — can be mitigated with campaigns | Medium Risk |
| Home Office segment | Most profitable — may be under-invested | Opportunity |
| Standard Class delivery (4.7 days avg) | Potential customer dissatisfaction risk | Medium Risk |
