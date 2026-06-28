# neharikab_2511729_part4_tableau_dashboad

## 1. Business Problem Summary

You are working as a business analyst for a retail leadership team. The leadership team wants an executive dashboard to monitor six key areas of business performance:

- **Sales performance** — Is revenue growing? Where and when?
- **Profitability** — Which categories, regions, and segments generate the most profit?
- **Customer segments** — How do Consumer, Corporate, and Home Office customers differ?
- **Category performance** — Which product categories and sub-categories are healthy vs at risk?
- **Shipping performance** — Does delivery speed affect customer satisfaction and returns?
- **Discount impact** — Are discounts helping volume or hurting margin?
- **Return patterns** — Where are returns concentrated and why?

The dashboard must not be a collection of random charts — it must tell a clear business story and support a specific decision: **where to invest and where to intervene to improve profitability**.

**Core business question:** Which areas of the business are generating healthy, sustainable profit, and which are structural drags that require immediate leadership attention?



## 2. Dataset Description

**File:** `data/dashboard_sales_data.xlsx`
**Sheet:** `dashboard_sales_data`

| Property | Value |
|---|---|
| Total rows | 4,200 orders |
| Date range | 1 Jan 2024 – 31 Dec 2025 |
| Unique customers | 4,096 |
| Unique orders | 4,200 |
| Total sales | $217,017,652 |
| Total profit | $33,306,313 |
| Overall profit margin | 15.3% |

**Field reference:**

| Field | Type | Description |
|---|---|---|
| `order_id` | String | Unique order identifier |
| `order_date` | Date | Date order was placed |
| `ship_date` | Date | Date order was shipped |
| `customer_id` | String | Unique customer identifier |
| `customer_segment` | Categorical | Consumer, Corporate, Home Office |
| `region` | Categorical | North, South, East, West |
| `state` | Geographic | Indian state name |
| `city` | Geographic | City of delivery |
| `category` | Categorical | Furniture, Office Supplies, Technology |
| `sub_category` | Categorical | 13 sub-categories (Tables, Chairs, Phones, etc.) |
| `product_name` | String | Full product name |
| `ship_mode` | Categorical | Same Day, First Class, Second Class, Standard Class |
| `sales` | Numerical | Order revenue in USD |
| `quantity` | Numerical | Number of units ordered |
| `discount` | Numerical | Discount applied (0.0 to 1.0 scale) |
| `profit` | Numerical | Profit on the order (can be negative) |
| `return_flag` | Binary (0/1) | 1 = order was returned |
| `delivery_days` | Numerical | Days from order to delivery |
| `customer_rating` | Numerical | Customer satisfaction rating (1–5 scale) |
| `campaign_channel` | Categorical | Organic, Paid, Social, Email, Referral (18 nulls) |

**Data assumptions documented:**
- `campaign_channel` has ~18 null values (0.4% of orders). These are excluded from channel-level analysis.
- `delivery_days` is computed from `ship_date` and `order_date`. Negative or zero values represent same-day fulfilment and are valid.
- `return_flag` is binary — the reason for return is not captured in this dataset.
- `profit` can be negative, representing orders where cost exceeded revenue (typically due to high discounts or returns).
- Geographic fields (`state`, `city`) are Indian locations. Regional grouping is North/South/East/West, not by geographic state boundary.



## 3. Tableau Workbook Description

**File:** `tableau/executive_dashboard.twbx`

The packaged workbook contains the data source embedded and the following sheets:

| Sheet Name | View Type | Purpose |
|---|---|---|
| Sales Trend | Line Chart | Monthly and yearly sales trend with YoY overlay |
| Regional Performance | Horizontal Bar Chart | Sales and profit by region, sortable |
| Category Profitability | Highlight Table | Profit margin by category and sub-category |
| Customer Segment View | Grouped Bar Chart | Sales, profit, and return rate by segment |
| Shipping Performance | Bar Chart | Delivery days and return rate by ship mode |
| Discount vs Profit | Scatter Plot | Order-level relationship between discount and profit |
| Return Analysis | Stacked Bar Chart | Return volume and rate by category and segment |
| Executive Dashboard | Dashboard | All views combined with KPI cards and filters |



## 4. Calculated Fields Created

All calculated fields are created in Tableau and available in the workbook.

| Calculated Field | Formula (Tableau Syntax) | Purpose |
|---|---|---|
| `Profit Margin` | `SUM([Profit]) / SUM([Sales])` | Core profitability KPI — used in KPI cards and highlight table |
| `Cost` | `SUM([Sales]) - SUM([Profit])` | Derived cost — used in cost analysis views |
| `Average Order Value` | `SUM([Sales]) / COUNTD([Order ID])` | Revenue efficiency metric — used in KPI cards and segment view |
| `Return Rate` | `SUM([Return Flag]) / COUNT([Order ID])` | Customer satisfaction proxy — used in guardrail KPI and return analysis |
| `Shipping Delay Bucket` | `IF [Delivery Days] <= 1 THEN "Same/Next Day (0-1d)" ELSEIF [Delivery Days] <= 3 THEN "Fast (2-3d)" ELSEIF [Delivery Days] <= 5 THEN "Standard (4-5d)" ELSE "Delayed (6+d)" END` | Categorises delivery performance for comparison |
| `Discount Bucket` | `IF [Discount] = 0 THEN "No Discount" ELSEIF [Discount] <= 0.10 THEN "1-10%" ELSEIF [Discount] <= 0.20 THEN "11-20%" ELSEIF [Discount] <= 0.30 THEN "21-30%" ELSE ">30%" END` | Groups discount depth into meaningful tiers for margin analysis |
| `Is Returned` | `[Return Flag] = 1` | Boolean for return filter and conditional formatting |



## 5. Dashboard Components

The Executive Dashboard (`executive_dashboard.twbx`) is built as a single-page dashboard with the following components:

**KPI Cards (top row — 4 cards):**
- Total Sales: $217M
- Total Profit: $33.3M
- Profit Margin: 15.3%
- Return Rate: 4.5%

**Charts (main body — 7 charts):**
1. Sales Trend Line Chart (top-left, wide) — monthly trend with 2024 vs 2025 overlay
2. Regional Performance Bar Chart (top-right) — sales and profit by region
3. Category Profitability Highlight Table (middle-left) — profit margin by sub-category, color-coded
4. Customer Segment Grouped Bar (middle-centre) — sales and return rate by segment
5. Shipping Performance Bar Chart (middle-right) — speed and return rate by ship mode
6. Discount vs Profit Scatter Plot (bottom-left) — individual order discount–profit relationship
7. Return Analysis Stacked Bar (bottom-right) — returns by category and segment

**Design specifications:**
- Color palette: Navy (#1F3864) for primary metrics, teal (#2E75B6) for secondary, red (#C00000) for risks
- Font: Arial throughout, size 11 for labels, 14 for chart titles, 18 for KPI values
- Layout: 1200 × 900px fixed-size dashboard, tiled layout



## 6. Filters and Interactions Used

| Filter | Type | Applied To |
|---|---|---|
| Region | Quick filter (multi-select checkbox) | All sheets |
| Category | Quick filter (multi-select checkbox) | All sheets |
| Customer Segment | Quick filter (multi-select checkbox) | All sheets |
| Order Date | Relative date range slider | All sheets |
| Ship Mode | Quick filter (multi-select checkbox) | Shipping and return views |
| Campaign Channel | Quick filter (single-select dropdown) | Sales trend and segment views |

**Dashboard Action (Filter Interaction):**
- Clicking any bar in the Regional Performance chart acts as a filter that updates all other charts on the dashboard to show only the selected region. This is implemented as a Dashboard Filter Action (Source: Regional Performance → Target: All Sheets).
- Clicking a sub-category in the Category Profitability highlight table filters the Discount vs Profit scatter to show only orders from that sub-category, enabling drill-down into specific profitability drivers.



## 7. Key Business Insights

Below are the top 5 insights surfaced by the dashboard. Full detail is in `outputs/business_insights.md`.

**1. Technology dominates profit (71% of total) at 18.2% margin** — Furniture delivers 24% of sales but only 10.7% of profit at 6.9% margin. Technology is the growth engine; Furniture is a margin drag.

**2. Discounts above 20% destroy margin** — Undiscounted orders earn 20.6% margin. Orders discounted above 30% produce a net loss (−5% margin). A hard discount cap at 20% would materially improve profitability.

**3. South region outperforms by $10M in sales** — All regions operate at similar margins (15.1–15.5%), making South's revenue lead a volume-of-business gap, not an efficiency gap. Replicating the South's go-to-market approach in East and West is the clearest revenue growth lever.

**4. Furniture has both the lowest margin and the highest return rate** — 7.7% return rate on a 6.9% margin category means a significant share of Furniture orders generates a net cost. Tables and Bookcases (5.7% margin each) should be reviewed for repricing or discontinuation.

**5. Home Office segment returns products most frequently (5.7%)** — Corporate customers have the most stable profile (15.2% margin, 4.0% return rate). Home Office leads in revenue but its elevated return rate is partially offsetting its margin advantage.



## 8. Dashboard Story Summary

The business is growing (4.3% YoY revenue growth) and profitable (15.3% margin), but the growth masks a structural profit quality problem. Technology is healthy and should be prioritised. Furniture is a volume story with thin margins and high returns — it needs intervention. Discounting above 20% is producing negative returns on some orders. The South region is the benchmark; East and West need targeted investment.

The dashboard tells this story through a connected set of views: the Sales Trend shows growth is real; Regional Performance shows it is uneven; Category Profitability shows where it is sustainable; Discount vs Profit shows the strategic risk; and Return Analysis shows where customer dissatisfaction is concentrated.

**Full narrative:** `outputs/dashboard_story.md`



## 9. Assumptions and Limitations

**Assumptions:**
- All monetary values are in USD. Currency conversion rates are not applied.
- `return_flag = 1` indicates a return occurred within the observation period — the return date is not captured.
- Negative `profit` values are treated as valid (e.g., heavily discounted or returned orders where cost exceeded revenue).
- Orders with null `campaign_channel` (18 orders, 0.4%) are excluded from channel analysis and treated as unattributed.
- `delivery_days` is calculated as `ship_date - order_date`. Processing time before shipment is included in this figure.

**Limitations:**
- **No customer lifetime value data** — the dataset is transaction-level. Repeat purchase rate, churn, and LTV cannot be calculated.
- **No full cost structure** — `profit` is available but the breakdown into cost of goods, logistics, and overhead is not. Margin comparisons may not reflect full economic profitability.
- **Return reasons not captured** — `return_flag` is binary only. Cannot distinguish quality defects, wrong items, expectations mismatch, or damage in transit.
- **Two-year window** — insufficient to separate structural trends from cyclical variation. Three or more years would enable more reliable seasonality modelling.
- **No inventory data** — high-performing sub-categories (Copiers, Accessories) may face supply constraints not visible in sales data.
- **Geographic granularity** — analysis at Region level masks state-level variation. Some states within a region may significantly outperform or underperform the regional average.



## 10. Screenshots Included

| File | Location | Contents |
|---|---|---|
| `full_dashboard.png` | `screenshots/` | Complete executive dashboard — all charts, KPI cards, and filters visible |
| `sales_trend_view.png` | `screenshots/` | Sales Trend sheet — monthly line chart with 2024 vs 2025 overlay |
| `regional_performance_view.png` | `screenshots/` | Regional Performance sheet — horizontal bar chart sorted by sales |
| `category_profitability_view.png` | `screenshots/` | Category Profitability highlight table — color-coded profit margin by sub-category |



