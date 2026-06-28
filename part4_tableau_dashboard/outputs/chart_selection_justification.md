# Chart Selection Justification
## Executive Dashboard — Retail Sales Performance (2024–2025)

---

## Overview

Each chart in the executive dashboard was selected based on a specific business question. This document explains the rationale, field usage, design principles applied, and mistakes deliberately avoided for every major visualization.

---

## 1. Sales Trend View — Line Chart (Monthly Sales and Profit Over Time)

**Business Question Answered:** How are total sales and profit changing month over month across 2024–2025?

**Why This Chart Type:** A line chart is the standard and most effective tool for visualizing continuous time-series data. It preserves the temporal order of data points and makes upward/downward trends, dips, and seasonal patterns immediately visible to a non-technical audience. A bar chart for 24 months would be cluttered; a line chart reads cleanly.

**Field Usage:**
- X-axis: Order Date (Month granularity)
- Y-axis: SUM(Sales) and SUM(Profit) as dual lines
- Color: Blue for Sales, Orange for Profit (visually distinct, non-alarming, business-neutral palette)
- Label: Year markers at January of each year to anchor the audience

**Design Principle Applied:** Data-ink ratio — only the line and axis labels are shown. No background gridlines except light horizontal reference lines. The dual line allows leadership to see whether profit is tracking with sales or diverging.

**Mistake Avoided:** Not using a stacked area chart (which would make it impossible to compare the two metrics independently) and not starting the Y-axis at a non-zero value (which would exaggerate the visual volatility of the trend).

---

## 2. Regional Performance View — Map + Bar Chart (Sales by State)

**Business Question Answered:** Which states and regions generate the most revenue and profit? Are there geographic concentration risks?

**Why This Chart Type:** A filled map (choropleth) gives leadership an immediate geographic intuition — they can see which states are dark (high performance) versus light (low performance) without reading numbers. The companion bar chart provides exact values and allows ranking. Together, they serve both spatial and analytical needs.

**Field Usage:**
- Map: State field (geographic dimension), SUM(Sales) on color
- Color: Sequential blue gradient — light blue for low sales, dark blue for high sales
- Bar Chart: Region on rows, SUM(Sales) and SUM(Profit) side-by-side bars
- Label: Direct labels on bars for exact values

**Design Principle Applied:** Hierarchy — the map provides the macro geographic picture, the bar chart provides the precise comparison. Leadership reads the map first (spatial), then drills into the bar chart (quantitative).

**Mistake Avoided:** Not using a bubble map (bubbles overlap on a dense geographic area like India) and not using red/green color coding on the map (red-green color blindness affects ~8% of men).

---

## 3. Category Profitability View — Bar Chart (Sub-Category Profit, Sorted Descending)

**Business Question Answered:** Which categories and sub-categories are driving profit — and which are dragging it down?

**Why This Chart Type:** A sorted horizontal bar chart is ideal for ranking comparisons across a moderate number of categories (14 sub-categories). It allows leadership to instantly see which bars extend into positive territory and which extend into negative territory (loss-making items). A treemap was considered but requires greater cognitive effort to read profit directionality.

**Field Usage:**
- Rows: Sub-Category
- Columns: SUM(Profit)
- Color: Diverging palette — green for positive profit, red for negative profit (semantically meaningful here: red = loss)
- Sort: Descending by profit so highest performers appear at the top
- Label: Profit values on each bar

**Design Principle Applied:** Diverging color to encode meaning — red/green is appropriate here because the axis itself passes through zero, making the semantic association (red = bad, green = good) accurate and unambiguous.

**Mistake Avoided:** Not using a pie chart (impossible to compare 14 sub-categories in a pie) and not using a treemap without a reference line (treemaps don't convey negative values).

---

## 4. Customer Segment View — Grouped Bar Chart (Segment vs. Sales/Profit)

**Business Question Answered:** Which customer segment — Consumer, Corporate, or Home Office — generates the highest sales and profit? Do segments perform differently by category?

**Why This Chart Type:** A grouped bar chart allows direct side-by-side comparison across three segments on two metrics (sales and profit). This is preferable to a pie chart (which only shows proportion, not absolute values) and more readable than a stacked bar when absolute comparison is the goal.

**Field Usage:**
- X-axis: Customer Segment
- Y-axis: SUM(Sales) and SUM(Profit) as grouped bars
- Color: One color per segment (consistent across the dashboard)
- Secondary breakdown: Category filter to see segment performance within Furniture, Technology, or Office Supplies

**Design Principle Applied:** Consistent color encoding — the same three colors used for segments on this sheet are reused on any other sheet that displays segment, maintaining visual continuity across the dashboard.

**Mistake Avoided:** Not using a stacked bar (which would conflate absolute and proportional comparison) and not using a donut chart (decorative, provides no additional analytical value over a bar).

---

## 5. Shipping Performance View — Bar Chart + Table (Ship Mode by Delivery Days and Profit)

**Business Question Answered:** Which shipping modes are most efficient? How does delivery speed relate to profitability and order volume?

**Why This Chart Type:** A bar chart for average delivery days by ship mode gives an immediate visual ranking of speed. A companion highlight table shows volume (order count) and profitability by ship mode side-by-side. Together, they allow leadership to assess the trade-off between cost, speed, and revenue.

**Field Usage:**
- Bar Chart: Ship Mode on rows, AVG(Delivery Days) on columns
- Color: Graduated — shorter delivery = darker green, longer = orange
- Table: Ship Mode × Metric (Sales, Profit, Order Count, Avg Delivery Days)
- Label: Values directly on bars

**Design Principle Applied:** Appropriate sorting — ship modes sorted by average delivery days (ascending) so the relationship between speed and mode is immediately clear.

**Mistake Avoided:** Not using a line chart for shipping mode (ship mode is a categorical dimension, not a time series — connecting points on a line would falsely imply a sequential relationship).

---

## 6. Discount vs. Profit View — Scatter Plot (Discount vs. Profit per Order)

**Business Question Answered:** Is there a relationship between discount percentage and order profitability? At what discount threshold does profit turn negative?

**Why This Chart Type:** A scatter plot is the only chart type that can reveal a correlation (or lack of correlation) between two continuous numerical variables simultaneously at the order level. Each dot represents one order, plotted by its discount on the X-axis and its profit on the Y-axis. The horizontal reference line at profit = 0 clearly delineates profitable from loss-making orders.

**Field Usage:**
- X-axis: Discount (continuous 0–35%)
- Y-axis: Profit (per order)
- Color: Category (Furniture, Technology, Office Supplies) — immediately shows which categories cluster in the loss zone
- Reference Line: Profit = 0 (dashed horizontal line)
- Tooltip: Order ID, Customer Segment, Category, Discount, Profit

**Design Principle Applied:** Zero-reference line — the dashed line at Profit = 0 is a critical anchor. Without it, leadership might not notice that some dots represent net losses.

**Mistake Avoided:** Not aggregating to average profit per discount band (which would hide the individual order-level variance) and not using a bar chart (which cannot show the bivariate correlation pattern).

---

## 7. Return Analysis View — Bar Chart (Return Rate by Category and Segment)

**Business Question Answered:** Which categories and customer segments have the highest return rates? Where is return-related margin leakage concentrated?

**Why This Chart Type:** A bar chart sorted by return rate allows clean comparison across categories and segments. A heatmap (highlight table) was considered but the small number of categories (3) does not justify the complexity. The bar chart is the most readable option for this audience.

**Field Usage:**
- X-axis: Return Rate (calculated field: SUM(Return Flag) / COUNT(Order Id))
- Y-axis: Category (and optionally Segment as secondary breakdown)
- Color: Single highlight color for bars exceeding the 5% threshold
- Label: Return rate percentage on each bar
- Reference Line: 5% threshold line to mark the acceptable limit

**Design Principle Applied:** Minimal clutter — no background color, no excessive gridlines. One reference line only where it communicates a meaningful threshold.

**Mistake Avoided:** Not using a pie chart for return rate (which would imply proportional share rather than rate) and not omitting the reference line (without a benchmark, leadership cannot assess whether 7.7% is concerning or normal).

---

## Summary of Design Principles Consistently Applied

| Principle | Application |
|---|---|
| Data-ink ratio | Removed all non-data elements (grid lines, borders, chart titles where tooltips suffice) |
| Consistent color encoding | Each segment and category uses the same color across all sheets |
| Sorted axes | All bar charts sorted by value (descending) unless time-ordering is required |
| Zero-baseline preservation | No Y-axis manipulation; all axes start at 0 or the natural data minimum |
| Semantic color use | Red only for losses/negatives; green for profit/positive; blue for sales (neutral) |
| Reference lines | Used sparingly and only where they add interpretive value (profit = 0, return = 5%) |
| Readable labels | All key values labeled directly on charts; no need to hover for the most important numbers |
