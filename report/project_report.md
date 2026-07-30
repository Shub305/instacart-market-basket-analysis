# Instacart Market Basket Analysis Report

---

## 1. Project Overview

This report presents an end-to-end analysis of the Instacart Online Grocery Shopping dataset, covering data preparation, exploratory data analysis (EDA), and market basket analysis using the Apriori algorithm. The goal of the project was to understand customer purchasing behavior, identify shopping trends, measure product loyalty through reorder patterns, and uncover meaningful product associations that can inform business strategy.

The analysis was performed in Python (Pandas, NumPy, Matplotlib, Mlxtend) within a Jupyter Notebook, and the key findings were further translated into an interactive Tableau dashboard to support business stakeholders in exploring the data themselves.

---

## 2. Business Objective

The primary objective of this project is to:

- Analyze customer purchasing behavior across the platform.
- Identify the most purchased products, aisles, and departments.
- Study reorder patterns to understand customer loyalty.
- Analyze shopping activity by day of week and hour of day.
- Discover frequently purchased product combinations using Market Basket Analysis.
- Translate the findings into actionable, data-driven business recommendations.

These objectives align with real-world use cases such as inventory planning, personalized product recommendations, cross-selling strategies, and promotional campaign design.

---

## 3. Dataset Description

The analysis uses the **Instacart Market Basket Analysis** dataset, which contains anonymized order-level transaction data from Instacart customers. The following source files were used:

| File | Description |
|---|---|
| `orders.csv` | Order-level metadata (order id, user id, day of week, hour of day, days since prior order) |
| `order_products__prior.csv` | Products in each customer's prior orders |
| `order_products__train.csv` | Products in each customer's most recent (training) order |
| `products.csv` | Product names mapped to aisle and department IDs |
| `aisles.csv` | Aisle ID to aisle name mapping |
| `departments.csv` | Department ID to department name mapping |

**Dataset scale (post-merge):**
- Total order-product rows analyzed: ~3.2 million
- Unique customers: 206,209
- Unique products: 49,677

Due to the scale of the full dataset, a **sampled subset (100,000 unique orders)** was used for the market basket analysis and Tableau dashboard to keep processing times and file sizes manageable, while the full dataset was used for department, aisle, product, and reorder-level EDA.

---

## 4. Data Preparation and Validation

Before analysis, the following steps were carried out to ensure data quality and consistency:

1. **Schema understanding** — reviewed dataset shape, column names, data types, and the relationships (grain, primary keys, and foreign keys) linking orders, products, aisles, and departments.
2. **Missing value assessment** — identified and handled missing values, most notably in `days_since_prior_order` for customers' first orders.
3. **Duplicate checks** — validated that order and product IDs did not contain unexpected duplicate records.
4. **Categorical validation** — confirmed that categorical fields (day of week, hour of day, department, aisle) contained only expected, valid values.
5. **Dataset merging** — joined `orders`, `order_products`, `products`, `aisles`, and `departments` into a single analysis-ready dataset, followed by post-merge validation to confirm row counts and key integrity were preserved.
6. **Sampling** — for the market basket analysis, 100,000 unique orders were randomly sampled (`random_state=42` for reproducibility) to reduce memory usage while preserving representative purchasing patterns.
7. **Product filtering** — for reorder rate analysis, only products with at least 100 total purchases were retained, preventing low-volume products from producing misleadingly high or low reorder rates.

---

## 5. Exploratory Data Analysis (EDA)

### 5.1 Product, Department, and Aisle Analysis
- **Bananas** and **Bag of Organic Bananas** were consistently the most purchased products overall, far ahead of other items.
- The **Produce** and **Dairy & Eggs** departments accounted for the highest purchase volumes, reflecting the platform's heavy use for fresh grocery staples.
- At the aisle level, **fresh fruits** and **fresh vegetables** were the top-performing aisles, reinforcing the produce-driven nature of customer baskets.

### 5.2 Reorder Pattern Analysis (Customer Loyalty)
- Products such as **Chocolate Love Bar** (92.1%), **Maca Buttercups** (90.0%), and **Benchbreak Chardonnay** (89.2%) exhibited the highest reorder rates among products with sufficient purchase volume, indicating strong repeat-purchase loyalty.
- Interestingly, the highest-reordered products were not always the most-purchased products — highlighting a difference between **popularity** (purchase count) and **loyalty** (reorder rate) that is valuable for retention-focused strategies.

### 5.3 Customer Purchase Behavior
- The average number of products per order across the sampled dataset was approximately **3–4 items**, though this varies by customer segment.
- Customer order counts followed a typical long-tail distribution, with a large base of occasional shoppers and a smaller group of highly frequent repeat customers.

### 5.4 Order Timing Patterns (Day & Hour)
- Order volume was highest on **Sunday and Monday**, gradually tapering off through the middle of the week.
- Shopping activity peaked between roughly **10 AM and 3 PM**, with a sharp drop-off overnight (12 AM–6 AM), consistent with typical daytime grocery-shopping behavior.

---

## 6. Market Basket Analysis

Market Basket Analysis was performed using the **Apriori algorithm** (via the `mlxtend` library) on the top 100 most-purchased products within the sampled 100,000-order dataset, in order to identify frequently co-purchased product combinations.

**Methodology:**
1. The dataset was pivoted into a one-hot encoded basket matrix (orders × products).
2. Frequent itemsets were generated using the Apriori algorithm.
3. Association rules were derived using **confidence** as the primary metric, with a **minimum confidence threshold of 0.3** selected to retain only stronger, more meaningful product relationships while filtering out weak or coincidental associations.

**Key association rules identified:**

| Rule | Support | Confidence | Lift |
|---|---|---|---|
| Organic Fuji Apple → Banana | 0.0145 | 0.377 | 1.85 |
| Honeycrisp Apple → Banana | 0.0122 | 0.357 | 1.75 |
| Cucumber Kirby → Banana | 0.0140 | 0.331 | 1.62 |
| Organic Raspberries → Bag of Organic Bananas | 0.0178 | 0.308 | 1.91 |
| Organic Avocado → Banana | 0.0230 | 0.309 | 1.53 |

**Observation:** Bananas appeared as the consequent in nearly every strong rule. This is expected given bananas' overall dominance as the single most-purchased product in the dataset — when an item is present in a very large share of all baskets, it naturally tends to co-occur frequently with almost anything else. This is why **lift** (not confidence alone) is the more meaningful metric for judging the strength of an association, since it adjusts for how common the consequent already is on its own.

---

## 7. Key Insights and Business Recommendations

### Key Insights
- Produce and dairy products drive the highest purchase volume on the platform.
- Reorder rate and purchase popularity are distinct signals — some lower-volume products show exceptionally strong customer loyalty.
- Shopping activity is concentrated in specific windows (weekends, daytime hours), which has direct operational implications.
- Fresh produce items — particularly bananas and apples — form the backbone of the platform's strongest product associations.

### Business Recommendations
1. **Recommend complementary products at checkout** — e.g., suggest bananas when a customer adds Organic Fuji Apples, Honeycrisp Apples, or Organic Raspberries to their cart.
2. **Create promotional bundles** for frequently co-purchased fresh produce combinations to encourage larger basket sizes.
3. **Improve product placement** — display strongly associated products together on category pages and search results to increase cross-selling opportunities.
4. **Personalize recommendations** using both reorder-rate and association-rule signals, rather than popularity alone, to better reflect genuine customer loyalty.
5. **Align staffing and inventory replenishment** with peak order-time windows (10 AM–3 PM, weekends) to reduce stockouts and improve fulfillment speed.

---

## 8. Dashboard Summary

To make these findings accessible to non-technical stakeholders, an interactive **Tableau dashboard** was built on top of the sampled dataset and the exported association rules table. The dashboard includes:

- **KPI summary cards**: Total Orders, Unique Customers, Unique Products, and Average Products per Order.
- **Top 10 Products, Top Departments, and Top Aisles** charts.
- **Reorder Rate by Product** (filtered to products with ≥100 purchases).
- **Orders by Hour** and **Orders by Day** charts to visualize shopping-time patterns.
- **Association Rules** chart showing the top rules by lift, with confidence and support as supporting detail.
- **Interactive filtering** by Department and Day of Week, allowing users to drill into specific segments of the data across all connected visuals.

🔗 *Dashboard link: [Add your published Tableau Public link here]*

---

## 9. Limitations

- The market basket analysis was performed on a **sampled 100,000-order subset** and limited to the **top 100 products**, rather than the full catalog — broader or more niche associations may not be captured.
- Reorder rate calculations exclude low-volume products (fewer than 100 total purchases) to avoid statistically unreliable rates, meaning some niche but genuinely loyal products are not represented.
- The dataset does not include pricing, promotions, or demographic information, limiting the analysis to purchase-pattern behavior only, without deeper customer-segment or revenue context.
- Association rules were generated using a fixed confidence threshold (0.3); results may shift meaningfully under different threshold or support settings.

---

## 10. Future Enhancements and Automation

- Perform **customer segmentation** using RFM (Recency, Frequency, Monetary) analysis to complement the reorder and basket-level findings.
- Build a **recommendation engine** using collaborative filtering, extending beyond rule-based association mining.
- Compare **Apriori vs. FP-Growth** algorithms for faster and more scalable association mining on the full dataset.
- Automate the data pipeline (extraction, cleaning, rule generation, and dashboard refresh) to support recurring, up-to-date reporting rather than a one-time analysis.
- Expand the Tableau dashboard with drill-down views (e.g., customer-level or department-level deep dives) as a second dashboard page.

---

## 11. Conclusion

This project analyzed the Instacart online grocery dataset to understand customer purchasing behavior and uncover actionable business insights through exploratory data analysis and market basket analysis. Produce and dairy products were found to drive the highest purchase volumes, while several products demonstrated notably high reorder rates, indicating strong customer loyalty independent of overall popularity. Shopping activity was shown to peak during weekends and daytime hours, offering clear guidance for inventory and staffing decisions.

Using the Apriori algorithm and association rule mining, meaningful product relationships were identified — particularly among fresh produce items, with bananas frequently appearing alongside apples, avocados, and other fruits. These associations, combined with the interactive Tableau dashboard built to support them, can help inform cross-selling strategies, personalized recommendations, promotional bundling, and broader inventory and operational planning.

Overall, this analysis demonstrates how transaction-level e-commerce data can be transformed into practical, business-relevant insights that support more informed, data-driven decision-making.
