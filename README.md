# 🛒 Superstore Sales — Exploratory Data Analysis (EDA)

A comprehensive pandas-based EDA on the Superstore Sales dataset, covering 50 structured analytical questions across sales performance, customer behavior, profitability, logistics, and statistical testing.

---

## 📁 Dataset

**File:** `Sales-Superstore-Dataset.xlsx`

The dataset contains transactional retail data with the following key fields:

| Field | Description |
|---|---|
| `order_id`, `order_date`, `ship_date` | Order tracking and timing |
| `customer_name`, `segment` | Customer identity and business segment |
| `region`, `state`, `city` | Geographic breakdown |
| `category`, `sub-category`, `product_name` | Product hierarchy |
| `sales`, `profit`, `discount` | Financial metrics |
| `ship_mode` | Shipping method used |

---

## 🛠️ Libraries Used

| Library | Purpose |
|---|---|
| `pandas` | Core data manipulation and analysis |
| `numpy` | Numerical operations and array handling |
| `matplotlib` | Base plotting framework |
| `seaborn` | Statistical data visualization |
| `scipy.stats` | Hypothesis testing and z-score analysis |

---

## 🔧 Data Preprocessing

- Loaded data from Excel using `pd.read_excel()`
- Removed duplicate rows with `drop_duplicates()`
- Standardized column names to `snake_case` (lowercased, spaces replaced with underscores)
- Derived new columns: `year`, `month_year`, `shipping_delay_days`, `shipping_days`, `profit_to_sales_ratio`, `z_scores_profit`

---

## 📊 Analysis Breakdown

### 1. Sales Performance & Trends (Q1, Q4, Q6, Q13, Q30, Q32)
- Computed **year-over-year (YoY) sales growth** using `pct_change()`
- Calculated **cumulative sales over time** using `cumsum()`
- Built **30-day and 7-day rolling averages** of daily sales using `rolling(window=...)`
- Visualized **monthly sales trends** and identified seasonal patterns
- Found the **single highest-performing month** historically

**Key Insight:** Sales show consistent end-of-year spikes (Oct–Dec), likely driven by holiday shopping and year-end business purchases. Yearly peaks grow over time, confirming overall business growth.

---

### 2. Customer Analysis (Q2, Q8, Q17, Q18, Q23, Q29, Q34, Q47, Q48)
- Identified the **top 10 customers by total sales** and their percentage contribution to company revenue
- Found **customers with more than 10 orders** using `.loc` and `.query()` approaches
- Computed **Customer Lifetime Value (CLV)** as total sales per customer
- **Segmented customers into quartiles** (Q1–Q4) based on total spend using `pd.qcut()`
- Determined the **most frequently purchased product per customer**
- Flagged customers **above the global average order value**
- Identified **single-category customers** (customers who never cross-purchased)
- Analyzed **repeat purchase frequency distribution**
- Flagged **customers with negative total profit contribution**

---

### 3. Product & Category Analysis (Q3, Q5, Q9, Q15, Q16, Q31, Q36, Q43, Q45, Q49)
- Identified the **sub-category with the highest profit margin** (Copiers)
- Found the **top 3 products within each category** using `groupby` + `rank()`
- Computed **median sales by category**
- Calculated **percentage sales contribution of each category** to total company sales
- Found the **most profitable product in each sub-category**
- Computed **sub-category sales as a percentage of their parent category**
- Analyzed **sales volatility by sub-category** using standard deviation and Coefficient of Variation (CV)
- Identified **categories with average discount exceeding 20%**
- Built a **summary table** of total sales, profit, and profit margin by category
- Visualized **sales distribution across categories** using bar plots

**Key Insight:** Technology drives the highest sales; Furniture has the lowest profit margin. Copiers and Machines have the highest absolute sales variance, but Binders and Supplies have the highest *relative* volatility (CV).

---

### 4. Geographic & Regional Analysis (Q10, Q14, Q19, Q25, Q26, Q33, Q44)
- Found the **state with the highest average order value**
- Identified the **top-performing category in each region**
- Ranked the **top 5 cities by total profit**
- Determined which region has the **highest average discount**
- Found the **top 5 most profitable states**
- Calculated **profit variance, mean, and standard deviation by region** with boxplot visualization
- Identified the **fastest-shipping region** based on average shipping days

---

### 5. Logistics & Shipping Analysis (Q7, Q21, Q35, Q38)
- Computed **average shipping delay by region**
- Identified **orders with unusually high shipping delays** (flagged 6–7 day shipments as operational delays; no statistical outliers found via 3σ rule due to constrained 0–7 day range)
- Summarized **total sales and profit by shipping mode**
- Calculated **average shipping time per shipping mode**

---

### 6. Discounts & Profitability (Q11, Q20, Q24, Q37, Q39)
- Identified **products that consistently generate negative profit**
- Computed **average discount by category**
- Calculated **profit-to-sales ratio per order** and ranked highest performers
- Flagged **orders where the discount exceeds the category average** (using both `merge` and `transform` approaches)
- Found the **customer segment generating the most total profit** (Consumer)

---

### 7. Time-Based & Seasonal Analysis (Q13, Q22, Q32, Q46)
- Visualized **monthly sales trends** to identify seasonality
- Tracked **monthly profit trends by category** over time
- Found the **historically highest-sales month**
- Identified the **most profitable month for each year**

---

### 8. Statistical Analysis (Q12, Q33, Q41, Q42)
- Built a **numeric correlation matrix** across financial features
- Calculated **profit variance across regions**
- Conducted **Welch's t-tests** comparing average profit between region pairs (East–West, South–Central, West–Central)
- Ran a **one-way ANOVA** across all four regions
- Computed **z-scores for profit** to detect statistical outliers

**Key Insight:**
- No statistically significant profit difference between East–West or South–Central pairs
- West vs. Central difference *is* statistically significant (p < 0.05)
- ANOVA confirms at least one region significantly differs from the others in average profit

---

### 9. Dashboard Summary (Q50)
- Built a **multi-panel summary** of top regions, top categories, and top 10 customers by sales with accompanying bar plots

---

## 🧰 Key Pandas Techniques Demonstrated

| Technique | Questions |
|---|---|
| `groupby` + `agg` / `sum` / `mean` | Throughout |
| `pct_change()` for YoY growth | Q1 |
| `cumsum()` for cumulative metrics | Q4 |
| `rolling(window=...)` for moving averages | Q6, Q30 |
| `rank()` within groups for top-N | Q5, Q14, Q16, Q22, Q46 |
| `pd.qcut()` for quartile binning | Q18 |
| `pd.pivot_table()` | Q28 |
| `transform()` for group-level broadcasting | Q31, Q37 |
| `nlargest()` / `nsmallest()` | Q10, Q19, Q26, Q44 |
| `.query()` and `lambda` with `.loc` | Q8, Q11, Q34, Q43 |
| `dt` accessor for date features | Q1, Q7, Q21 |
| `merge()` for joining aggregations | Q37 |
| `assign()` for inline column creation | Q15 |
| `scipy.stats.ttest_ind` + `f_oneway` | Q41 |
| `scipy.stats.zscore` | Q42 |

---

## 📌 Top Insights Summary

| Area | Insight |
|---|---|
| **Sales Growth** | Consistent YoY growth with strong Q4 seasonality |
| **Top Category** | Technology leads in sales; Furniture lags in profitability |
| **Best Sub-Category Margin** | Copiers have the highest profit margin |
| **Highest Volatility** | Binders & Supplies have the most inconsistent relative demand |
| **Loss-Making Products** | Several products generate consistent negative profit — candidates for discontinuation |
| **Customer Segmentation** | Most customers cluster in lower spend quartiles; a small group drives outsized revenue |
| **Regional Profitability** | West and Central regions show statistically different average profit |
| **Discounting Risk** | Heavy discounting in certain categories is eroding margins |
| **Shipping** | Shipping delays are operationally bounded (0–7 days); no extreme statistical outliers |

---

## 🚀 How to Run

1. Clone the repository
2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn scipy openpyxl
   ```
3. Place `Sales-Superstore-Dataset.xlsx` in the same directory as the notebook
4. Launch Jupyter and open `Superstore_sales_EDA.ipynb`:
   ```bash
   jupyter notebook Superstore_sales_EDA.ipynb
   ```

---

## 📂 Repository Structure

```
├── Superstore_sales_EDA.ipynb   # Main analysis notebook
├── Sales-Superstore-Dataset.xlsx # Source data
└── README.md                    # This file
```
