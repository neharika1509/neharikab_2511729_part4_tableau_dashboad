# Chart Selection Justification

**Dashboard:** Executive Sales Performance Dashboard
**Purpose:** Justify every major chart type used in the dashboard against the business question it answers, design principle applied, and mistakes avoided.

---

## Chart 1 — Sales Trend Over Time: Line Chart

**Business Question:** How are total sales changing over time? Are we growing month-on-month and year-on-year?

**Why this chart type is appropriate:** A line chart is the standard choice for continuous time-series data. It makes trend direction (upward, downward, flat) immediately readable and allows comparison of multiple years on the same axis. The eye naturally follows the line and detects peaks, troughs, and seasonality without needing to read individual values.

**Fields used:**
- X-axis: Order Date (Month/Year)
- Y-axis: SUM(Sales)
- Color: Year (to overlay 2024 vs 2025 for YoY comparison)
- Filter: Date range filter, Region filter

**Design principle applied:** Clear hierarchy — Sales is the primary measure and is given the full vertical axis. Year is distinguished by color rather than separate charts, reducing cognitive load. Gridlines are minimised to avoid clutter. The chart starts at zero on the Y-axis to avoid misleading magnitude perception.

**Mistake avoided:** Did not use a bar chart for monthly trend — bar charts are appropriate for discrete categorical comparisons, not continuous temporal trends. Did not truncate the Y-axis (e.g., starting at $5M instead of $0), which would exaggerate the visual magnitude of small month-to-month changes.

---

## Chart 2 — Regional Performance: Bar Chart (Horizontal)

**Business Question:** Which region generates the most sales and profit? How do regions compare?

**Why this chart type is appropriate:** A horizontal bar chart is ideal for comparing a discrete set of named categories (regions) on a single measure. Region names read naturally on the left axis without rotation. Bars can be sorted descending to immediately communicate rank order. Adding a second measure (profit) as a second bar or color-coded overlay enables direct comparison without switching charts.

**Fields used:**
- X-axis: SUM(Sales), SUM(Profit)
- Y-axis: Region
- Color: Measure (Sales vs Profit — dual-measure bars)
- Sort: Descending by Sales

**Design principle applied:** Appropriate sorting — bars are sorted from highest to lowest sales so the best-performing region is at the top and rank is visually immediate. Consistent color usage — Sales and Profit use a consistent two-color palette throughout the dashboard. Labels are shown on bars to avoid requiring the viewer to reference the axis for exact values.

**Mistake avoided:** Did not use a pie chart — pie charts are poor for comparing four similarly-sized regions because humans struggle to compare arc lengths and angles. Did not use 3D bars, which distort relative heights and serve no informational purpose.

---

## Chart 3 — Category and Sub-Category Profitability: Highlight Table (Heat Map)

**Business Question:** Which categories and sub-categories drive profit or losses? Where are the margins weakest?

**Why this chart type is appropriate:** A highlight table (also called a heat map or cross-tab with color encoding) is ideal when comparing many items across multiple dimensions simultaneously. It shows both the value and the relative magnitude through color intensity, making it immediately apparent which cells are high-performing (dark positive color) and which are problematic (red or light color). For 13 sub-categories across 3 categories, a bar chart would require too much vertical space.

**Fields used:**
- Rows: Category, Sub-Category
- Columns: Metric (Sales, Profit, Profit Margin)
- Color: Profit Margin (diverging color scale — green for high margin, red for low/negative)
- Label: Profit Margin % displayed in each cell

**Design principle applied:** Meaningful colors — a diverging red-to-green color scale is used where green = high margin (good) and red = low/negative margin (risk). This is intuitive and matches business convention. The color midpoint is set at the company average margin (15.3%) so viewers can immediately see which sub-categories are above or below the company benchmark.

**Mistake avoided:** Did not use a single color scale (e.g., light blue to dark blue) — a single-hue scale does not effectively communicate the direction of a problem. Did not skip sorting — sub-categories are sorted within each category by profit margin ascending so the worst performers are always visible at the top.

---

## Chart 4 — Customer Segment Comparison: Grouped Bar Chart

**Business Question:** How do the three customer segments (Consumer, Corporate, Home Office) compare on sales, profit, and return rate?

**Why this chart type is appropriate:** A grouped bar chart allows direct side-by-side comparison of multiple measures across a small number of named categories. With only three segments and three measures, grouped bars are clean and readable. Each group (segment) has bars for Sales, Profit, and Return Rate, making it easy to see whether a segment that leads on sales also leads on profitability.

**Fields used:**
- X-axis: Customer Segment
- Y-axis: SUM(Sales) (primary axis) / AVG(Return Flag) as % (secondary axis)
- Color: Measure type
- Filter: Region, Category, Date

**Design principle applied:** Focus on business interpretation — the chart does not simply show raw values but is annotated with the margin percentage and return rate for each segment, making the business implication clear without additional lookup. Minimal clutter — background colors, unnecessary grid lines, and decorative elements are removed.

**Mistake avoided:** Did not use a stacked bar chart — stacking makes it impossible to compare the absolute height of individual segments within the stack. Did not combine return rate and sales on the same Y-axis without a secondary axis, which would produce misleading scale comparisons.

---

## Chart 5 — Discount vs Profit: Scatter Plot

**Business Question:** Does offering larger discounts lead to lower profitability? What is the relationship between discount depth and profit per order?

**Why this chart type is appropriate:** A scatter plot is the correct chart type for showing the relationship between two continuous numerical variables. Each point represents one order, plotted by its discount (X) and profit (Y). The scatter reveals the overall direction of the relationship, the spread, and any outliers or clusters. A trend line can be overlaid to quantify the relationship direction (negative slope confirms the inverse relationship).

**Fields used:**
- X-axis: Discount (continuous 0–1 scale)
- Y-axis: Profit (continuous, can be negative)
- Color: Category (to see if the relationship differs by category)
- Size: Sales (to weight by order value)
- Filter: Category, Segment, Region

**Design principle applied:** Avoidance of misleading scales — both axes start at natural zero (or the actual minimum for profit, which can be negative). The trend line is included to make the relationship explicit rather than asking the viewer to infer it from the scatter cloud alone. Color by Category allows the viewer to see whether the discount-profit relationship is consistent across categories or driven by one.

**Mistake avoided:** Did not use a bar chart — a bar chart of "average profit by discount bucket" would hide individual order variance and the scatter of the data. Did not plot too many points without color or size differentiation, which would result in an unreadable cloud with no actionable insight.

---

## Chart 6 — Shipping Performance: Bar Chart with Secondary Metric

**Business Question:** Which shipping mode delivers products fastest? Does delivery speed correlate with returns or customer satisfaction?

**Why this chart type is appropriate:** A horizontal bar chart comparing four shipping modes on average delivery days and return rate is clear, scannable, and allows immediate rank comparison. Adding return rate as a secondary bar or overlay connects the operational metric (speed) to the customer outcome metric (returns), telling a complete story in one view.

**Fields used:**
- Rows: Ship Mode
- Columns: AVG(Delivery Days) (primary), AVG(Return Flag) as % (secondary)
- Color: Ship Mode (consistent with other shipping-related charts)
- Sort: Ascending by Delivery Days (fastest to slowest)
- Filter: Date, Region

**Design principle applied:** Readable titles — the chart title is "Shipping Mode Performance: Speed vs Return Rate" which communicates both what is shown and why it matters. Proper labels — actual values are shown on each bar to avoid the need to reference the axis for precise values. Appropriate sorting — sorted by speed so viewers see the modes in a logical sequence.

**Mistake avoided:** Did not use a line chart — ship mode is a categorical variable, not a continuous one, so connecting points with a line would imply a meaningless continuous relationship. Did not omit the return rate — showing only delivery days would answer only half the business question.

---

## Chart 7 — Return Analysis: Stacked Bar Chart by Category and Segment

**Business Question:** Which categories and customer segments have the highest return rates? Where is the return risk concentrated?

**Why this chart type is appropriate:** A stacked bar chart showing return count by category, color-coded by segment, allows the viewer to see both the total return volume per category and the contribution of each segment to that total. This answers two questions simultaneously: which category returns most, and which segment drives those returns.

**Fields used:**
- X-axis: Category
- Y-axis: SUM(Return Flag) — count of returned orders
- Color: Customer Segment
- Label: Return rate % (as an annotation)
- Filter: Region, Ship Mode, Date

**Design principle applied:** Clear hierarchy — Category is the primary grouping (X-axis), Segment is the secondary breakdown (color). The most important number (return rate %) is annotated directly on the chart rather than hidden in a tooltip. Color usage is consistent with the segment colors used in other dashboard charts.

**Mistake avoided:** Did not use a 100% stacked bar — a 100% stacked bar would show segment composition but lose the absolute volume information, which is equally important for this business question. Did not use a pie chart for each category — small multiples of pies are very difficult to compare and would fragment the comparison.

---

## Summary: Chart Selection Principles Applied

| Principle | How Applied |
|---|---|
| Chart type matches question type | Trend → Line; Comparison → Bar; Relationship → Scatter; Composition → Highlight Table |
| Consistent color usage | Same color palette used for Categories, Segments, and Regions across all charts |
| Axes start at zero | No truncated axes that exaggerate differences |
| Sort communicates rank | All categorical charts sorted by the primary measure descending |
| Labels reduce eye travel | Key values annotated on charts; axis tick labels are supplementary |
| Filters are contextual | All dashboard filters apply to all charts simultaneously via dashboard filter actions |
| Minimal clutter | Gridlines, borders, and background colors removed or minimised |
| No decorative charts | Every chart answers a specific business question — no chart is present for visual variety |
