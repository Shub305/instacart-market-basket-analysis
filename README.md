# 🛒 Instacart Market Basket Analysis

## 📌 Project Overview

This project analyzes the Instacart Online Grocery Shopping Dataset to understand customer purchasing behavior, reorder patterns, shopping trends, and product associations. Using Exploratory Data Analysis (EDA) and Market Basket Analysis with the Apriori algorithm, the project uncovers actionable business insights that can support inventory planning, product recommendations, cross-selling, and promotional strategies.

---

## 🎯 Business Objective

The primary objective of this project is to:

* Analyze customer purchasing behavior.
* Identify the most purchased products, aisles, and departments.
* Study reorder patterns to understand customer loyalty.
* Analyze shopping activity by day and hour.
* Discover frequently purchased product combinations using Market Basket Analysis.
* Provide business recommendations based on data-driven insights.

---

## 📂 Dataset

This project uses the **Instacart Market Basket Analysis** dataset.

The following files were used:

* `orders.csv`
* `order_products__prior.csv`
* `order_products__train.csv`
* `products.csv`
* `aisles.csv`
* `departments.csv`

---

## 🔄 Project Workflow

1. Data Loading
2. Data Cleaning & Validation
3. Exploratory Data Analysis (EDA)
4. Customer Purchase Behavior Analysis
5. Product, Department & Aisle Analysis
6. Reorder Pattern Analysis
7. Order Pattern Analysis (Day & Hour)
8. Market Basket Analysis (Apriori Algorithm)
9. Association Rule Mining
10. Business Recommendations

---

## 🛠️ Tools & Technologies

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Mlxtend (Apriori Algorithm)
* Jupyter Notebook
* Tableau

---

## 📊 Key Insights

* Produce and dairy products accounted for the highest purchase volume.
* Several products exhibited high reorder rates, indicating strong customer loyalty.
* Shopping activity peaked during weekends and daytime hours.
* Organic fruits and fresh produce frequently appeared together in customer baskets.
* Association Rule Mining identified meaningful product relationships that can improve recommendation systems and cross-selling strategies.

---

## 💼 Business Recommendations

* Recommend complementary products during checkout.
* Create promotional bundles for frequently purchased product combinations.
* Improve product placement using association rules.
* Personalize customer recommendations based on purchasing behavior.
* Use reorder insights for inventory planning and demand forecasting.

---

## 📊 Project Visualizations

### Top 10 Purchased Products

🔗[Top Products](images/top_10_purchased_products.png)

* Bananas, organic strawberries, and bagged organic salad greens are the most frequently purchased items overall, highlighting the dominance of fresh produce in customer baskets.

---

### Orders by Hour

🔗[Orders by Hour](images/orders_by_hour.png)

* Order volume peaks between **10 AM and 3 PM**, with activity dropping sharply overnight — useful for staffing and delivery capacity planning.

---

### Reorder Rate

🔗[Reorder Rate](images/reorder_rate_by_products.png)

* Products like **Chocolate Love Bar** and **Maca Buttercups** show reorder rates above 90%, indicating strong customer loyalty and repeat-purchase behavior for these items.

---

### Market Basket Analysis

🔗[Association Rules](images/association_rules.png)

🔗 [View Interactive Dashboard on Tableau Public](https://public.tableau.com/views/Instacart_Market_Basket_Analysis/Dashboard4?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

* Strong associations emerged between complementary produce items — for example, customers who buy **Organic Fuji Apples** are highly likely to also purchase **Bananas** in the same order, suggesting opportunities for cross-selling and bundling.

## 📁 Repository Structure

```text
instacart-market-basket-analysis/
│
├── data/
├── notebooks/
├── outputs/
├── dashboard/
├── README.md
├── requirements.txt
└── .gitignore
```

---

## 🚀 Future Improvements

* Perform customer segmentation using RFM analysis.
* Build a recommendation system using collaborative filtering.
* Compare Apriori with FP-Growth for faster association mining.
* Deploy an interactive dashboard for business users.

---

## 👨‍💻 Author

**Shubham Kumar**

Aspiring Data Analyst | Python | SQL | Tableau | Data Visualization
