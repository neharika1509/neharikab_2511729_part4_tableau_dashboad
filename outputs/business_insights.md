# Business Insights

**Source:** Executive Dashboard — Retail Sales Data (2024–2025)
**Dataset:** 4,200 orders | $217M total sales | $33.3M total profit

---

## Calculated Fields Used in This Analysis

| Calculated Field | Formula | Purpose |
|---|---|---|
| `Profit Margin` | `SUM([Profit]) / SUM([Sales])` | Measures how efficiently sales convert to profit |
| `Cost` | `SUM([Sales]) - SUM([Profit])` | Derives total cost from available fields |
| `Average Order Value` | `SUM([Sales]) / COUNT([Order ID])` | Measures revenue per transaction |
| `Return Rate` | `SUM([Return Flag]) / COUNT([Order ID])` | Proportion of orders returned |
| `Shipping Delay Bucket` | `IF [Delivery Days] <= 1 THEN "Same/Next Day" ELSEIF [Delivery Days] <= 3 THEN "Fast (2-3 days)" ELSEIF [Delivery Days] <= 5 THEN "Standard (4-5 days)" ELSE "Delayed (6+ days)" END` | Categorises delivery speed for comparison |

---

## Insight 1 — Sales Trend: Consistent Year-over-Year Growth with Q1 and Q3 Peaks

**Observation:** Total sales grew from $106.2M in 2024 to $110.8M in 2025, a 4.3% year-over-year increase. Monthly peaks occur in January–March and July–August.

**Data Evidence:**
- 2024 total: $106,241,026
- 2025 total: $110,776,626
- YoY growth: +4.3%
- Highest months in 2025: July ($10.7M), August ($10.9M), March ($10.2M)

**Business Interpretation:** The business is growing steadily. Seasonal peaks in Q1 and Q3 suggest either campaign-driven spikes or natural demand cycles (possibly tied to financial year planning for corporate buyers and back-to-school/festive season for consumers).

**Recommended Action:** Plan inventory, staffing, and marketing campaigns around the Q1 and Q3 peaks to avoid stockouts and maximise conversion during high-demand windows. Investigate Q2 dip (April: $7.2M) — is this a market cycle or a missed opportunity?

---

## Insight 2 — Regional Performance: South Dominates, East and West Underperform

**Observation:** The South region leads all regions in both sales and profit. East and West are nearly identical and trail by approximately $15M in sales.

**Data Evidence:**
- South: $64.7M sales, $10.0M profit (15.4% margin)
- North: $54.6M sales, $8.3M profit (15.2% margin)
- West: $48.9M sales, $7.4M profit (15.1% margin)
- East: $48.9M sales, $7.6M profit (15.5% margin)

**Business Interpretation:** All four regions operate at similar profit margins (15.1–15.5%), so the gap is a revenue volume problem, not a profitability problem. The South is generating more transactions or higher-value orders, not just more efficiently.

**Recommended Action:** Analyse the South region's customer mix, campaign channel performance, and sales team structure. Use findings to build a targeted go-to-market plan for East and West markets to close the ~$15M revenue gap.

---

## Insight 3 — Category Profitability: Technology Carries the Business, Furniture Is a Risk

**Observation:** Technology generates 71% of total profit from 71% of total sales, at a healthy 18.2% margin. Furniture generates 24% of sales but only 10.7% of profit at a dangerously thin 6.9% margin.

**Data Evidence:**
- Technology: $153.9M sales, $28.0M profit (18.2% margin)
- Furniture: $51.6M sales, $3.6M profit (6.9% margin)
- Office Supplies: $11.5M sales, $1.7M profit (14.8% margin)

**Business Interpretation:** Furniture is a volume contributor that consumes significant operational capacity (logistics, warehousing, customer service) while delivering less than 7 cents profit per dollar of revenue. Any cost increase, return spike, or discount event in Furniture can quickly erode margins.

**Recommended Action:** Commission a detailed Furniture cost-to-serve analysis. Evaluate whether Tables and Bookcases (5.7% margin each) should be repriced, repositioned, or phased out in favour of higher-margin Technology products.

---

## Insight 4 — Sub-Category Profitability: Furniture Sub-categories Are the Bottom Performers

**Observation:** The four lowest-margin sub-categories are all Furniture or Furniture-adjacent. Technology sub-categories occupy the top four spots.

**Data Evidence:**
- Tables: 5.7% margin | Bookcases: 5.7% | Furnishings: 7.9% | Chairs: 8.2%
- Phones: 18.5% | Accessories: 18.3% | Machines: 18.1% | Copiers: 18.0%

**Business Interpretation:** The margin gap between best and worst sub-categories is 12.8 percentage points. This is a portfolio composition problem — if the product mix shifts even slightly toward Technology sub-categories, overall company margin improves materially.

**Recommended Action:** Set a sub-category-level profit margin floor (e.g., 10%) as a portfolio management rule. Any sub-category consistently below this floor should undergo a pricing or discontinuation review within one quarter.

---

## Insight 5 — Customer Segment Behavior: All Segments Are Similar in Volume, Home Office Leads in Revenue

**Observation:** The three customer segments (Consumer, Corporate, Home Office) are remarkably balanced in both sales volume and profitability. Home Office leads narrowly in both sales and profit.

**Data Evidence:**
- Home Office: $74.5M sales, $11.6M profit (15.5% margin)
- Consumer: $71.9M sales, $11.0M profit (15.3% margin)
- Corporate: $70.6M sales, $10.7M profit (15.2% margin)

**Business Interpretation:** No single segment is significantly outperforming or underperforming on revenue. However, Home Office has the highest return rate (5.7%), which is partially offsetting its margin advantage. Corporate has the most stable profile — strong revenue, good margin, lowest return rate among the three.

**Recommended Action:** Investigate the root cause of Home Office returns. If product descriptions or sizing/compatibility information can be improved, reducing the return rate from 5.7% to the Corporate level of 4.0% would meaningfully improve Home Office profitability.

---

## Insight 6 — Discount Impact: Every Discount Tier Above 10% Significantly Erodes Margin

**Observation:** There is a clear and consistent inverse relationship between discount depth and profit margin. Orders with no discount earn 20.6% margin; orders discounted above 30% generate a net loss.

**Data Evidence:**
- No discount: 20.6% margin | $13.5M profit
- 1–10% discount: 17.0% margin | $9.8M profit
- 11–20% discount: 13.6% margin | $6.6M profit
- 21–30% discount: 8.0% margin | $3.5M profit
- >30% discount: −5.0% margin | −$102K net loss

**Business Interpretation:** The business is giving away margin through discounting, likely to drive volume or retain customers. The practice of deep discounting (>20%) is not just reducing margin — it's producing negative returns on 2% of all orders. The correlation between discount and profit is −0.27, confirming a statistically meaningful negative relationship.

**Recommended Action:** Implement a hard cap on discounts at 20% unless approved by senior leadership on a case-by-case basis. Create a discount approval workflow and track the margin impact of approved exceptions quarterly.

---

## Insight 7 — Shipping & Delivery Performance: Standard Class Offers Best Margin Efficiency

**Observation:** Same Day shipping has the highest average profit per order, but Standard Class offers a strong profit per order at significantly lower fulfilment cost and is used for the majority of orders.

**Data Evidence:**
- Same Day: avg $9,102 profit/order, 0.40 avg delivery days (669 orders)
- Second Class: avg $8,261 profit/order, 2.68 avg delivery days (1,566 orders)
- First Class: avg $7,364 profit/order, 1.77 avg delivery days (1,066 orders)
- Standard Class: avg $7,839 profit/order, 4.71 avg delivery days (1,666 orders — most used)

**Business Interpretation:** Same Day shipping is used for high-value orders, which naturally produces higher profit per order — but this may reflect order value selection rather than a shipping-mode-driven profit improvement. Standard Class handles the most volume efficiently. Delayed orders (6+ days) show a slightly higher return rate, suggesting delivery speed does affect customer satisfaction.

**Recommended Action:** Audit orders currently shipped First Class — if order value does not justify the premium, downgrade to Standard Class to reduce logistics costs. Set a minimum order value threshold for Same Day shipping eligibility.

---

## Insight 8 — Return Patterns: Furniture Returns Are a Dual Risk — High Rate in a Low-Margin Category

**Observation:** Furniture has both the lowest profit margin (6.9%) and the highest return rate (7.7%) of all categories. This combination makes Furniture the highest-risk category in the portfolio.

**Data Evidence:**
- Furniture return rate: 7.7%
- Office Supplies return rate: 3.7%
- Technology return rate: 3.0%
- Overall return rate: 4.5%

**Business Interpretation:** In a category already operating at thin margins, a 7.7% return rate means a disproportionate share of Furniture orders generate a net cost rather than profit. Returns in Furniture likely involve high logistics costs (large items, reverse fulfilment) which may not be fully captured in the profit figure available. The combination of low margin + high returns + high logistics cost makes Furniture a structural drag on overall profitability.

**Recommended Action:** Immediately tag Furniture returns by reason code (quality defect, wrong item, expectation mismatch, damaged in transit). Use this data to target the biggest return driver first. If expectation mismatch is the primary cause, improve product descriptions, imagery, and size/dimension information on the product pages.

---

## Insight 9 — Business Risk: Referral Channel Customers Return Products Most Frequently

**Observation:** Customers acquired through the Referral channel have the highest return rate (6%) among all campaign channels, and Organic channel customers have the second-lowest (4%).

**Data Evidence:**
- Referral: $21.2M sales, 15.7% margin, 6.0% return rate
- Email: $34.5M sales, 15.5% margin, 5.0% return rate
- Paid: $40.1M sales, 15.1% margin, 5.0% return rate
- Social: $31.1M sales, 15.8% margin, 4.0% return rate
- Organic: $88.8M sales, 15.1% margin, 4.0% return rate

**Business Interpretation:** The Referral channel's high return rate suggests that referred customers may be arriving with misaligned expectations — either because the referrer oversold the product, or because referral incentives attract less qualified buyers. Meanwhile, Organic channel drives 41% of all revenue at a competitive margin and healthy return rate, making it the most reliable and scalable acquisition channel.

**Recommended Action:** Review referral programme mechanics — are incentives attracting genuine buyers or opportunistic sign-ups? Consider adding a minimum order value or product category restriction to referral rewards. Double down on Organic channel investment.

---

## Insight 10 — Business Opportunity: Campaign Channel Mix Has Significant Untapped Potential

**Observation:** Organic channel generates $88.8M in sales — more than Paid, Social, and Referral combined ($92.4M) but is almost certainly the lowest-cost channel. Paid channel generates $40.1M but may carry significant acquisition cost not visible in this dataset.

**Data Evidence:**
- Organic: $88.8M | 15.1% margin | 4.0% return rate
- Paid: $40.1M | 15.1% margin | 5.0% return rate
- Email: $34.5M | 15.5% margin | 5.0% return rate
- Social: $31.1M | 15.8% margin | 4.0% return rate
- Referral: $21.2M | 15.7% margin | 6.0% return rate

**Business Interpretation:** Social channel offers the highest profit margin (15.8%) and a low return rate (4.0%) at $31.1M in sales — suggesting it is an underinvested channel with strong quality customers. Email also performs well at 15.5% margin. If Social and Email acquisition costs are lower than Paid, reallocating budget toward these channels could improve net profitability.

**Recommended Action:** Conduct a channel-level CAC (Customer Acquisition Cost) analysis to calculate true channel ROI. If Social and Email show lower CAC with comparable or better margin, shift budget allocation within 30 days.
