# 🏬 Superstore Sales Analysis | End-to-End Data Engineering on Snowflake

![Snowflake](https://img.shields.io/badge/Platform-Snowflake-29B5E8?style=for-the-badge&logo=snowflake&logoColor=white)
![SQL](https://img.shields.io/badge/Language-SQL-orange?style=for-the-badge&logo=postgresql&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
![Dataset](https://img.shields.io/badge/Records-51,252-blue?style=for-the-badge)

---

## 📌 Project Summary

| Item | Detail |
|------|--------|
| **Domain** | E-Commerce / Retail (Global Superstore) |
| **Platform** | Snowflake Cloud Data Warehouse |
| **Total Records** | 51,252 transactions |
| **Total Sales** | $12.63M |
| **Total Profit** | $1.46M (11.60% margin) |
| **Date Range** | 2011 – 2014 |
| **Approach** | Ingestion → Cleaning → Transformation → Statistical Analysis → BI View |
| **Queries** | 30+ analytical SQL queries (9 sections) |

---

## 🏗️ Architecture — Medallion-Style Pipeline

```
┌────────────────────────────────────────────────────────────────────────────────┐
│                        END-TO-END DATA PIPELINE                                │
│                                                                                │
│  ┌──────────┐    ┌───────────────┐    ┌──────────────┐    ┌───────────────┐   │
│  │  BRONZE  │───▶│    SILVER     │───▶│     GOLD     │───▶│   INSIGHTS    │   │
│  │ (Raw)    │    │ (Cleaned)     │    │ (Enriched)   │    │ (Analytics)   │   │
│  └──────────┘    └───────────────┘    └──────────────┘    └───────────────┘   │
│                                                                                │
│  • 51,252 rows    • Date conversion   • SPU metrics       • KPIs & margins   │
│  • Raw CSV        • Encoding fix      • Discount bands    • Statistical      │
│  • Global data    • Dedup (38 rows)   • Profit flags      • Power BI view    │
│  •                • Whitespace trim   • IQR outliers      • Recommendations  │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘
```

---

## 📂 Project Structure

```
superstore-data-engineering/
│
├── 📄 superstore_README.md        ← Project documentation (you are here)
├── 📄 superstore_queries.sql      ← All SQL queries (9 sections, 30+ queries)
│
├── 🔹 Bronze Layer                ← Raw superstore global dataset
├── 🔹 Silver Layer                ← Cleaned (dates, encoding, dedup, trim)
├── 🔹 Gold Layer                  ← SPU, discount bands, outlier flags, BI view
└── 🔹 Analytics Layer             ← Segment, category, region, time, product insights
```

---

## 📊 Dataset Overview

| KPI | Value |
|-----|-------|
| 📦 Total Rows | **51,252** |
| 🛒 Total Orders | **25,035** |
| 👥 Total Customers | **4,873** |
| 📋 Total Products | **10,292** |
| 💰 Total Sales | **$12.63M** |
| 📈 Total Profit | **$1.46M** |
| 📊 Profit Margin | **11.60%** |

---

## 🔧 Pipeline Execution Steps

### 🟤 Step 1 — Bronze Layer (Raw Ingestion)
```sql
-- Global Superstore dataset loaded
-- 51,252 rows across multiple markets, segments, and categories
SELECT * FROM SUPERSTORE LIMIT 10;
```

### ⚪ Step 2 — Silver Layer (Data Cleaning)

| Cleaning Task | Method | Impact |
|---------------|--------|--------|
| Date Format | VARCHAR (`DD-MM-YYYY`) → DATE | All date columns fixed |
| Encoding Fix | Product name corruption repair | 278 rows corrected |
| Duplicate Removal | Exact row dedup | 38 duplicates removed |
| Market Standardization | Inconsistent market names unified | Clean categorical data |
| Whitespace Trim | `TRIM()` on all text columns | Clean text fields |

### 🟡 Step 3 — Gold Layer (Feature Engineering & Metrics)
```sql
-- Sales Per Unit (SPU)
SPU = SALES / QUANTITY

-- Discount Bands
CASE
    WHEN DISCOUNT = 0 THEN 'No Discount'
    WHEN DISCOUNT <= 0.2 THEN 'Low'
    WHEN DISCOUNT <= 0.4 THEN 'Medium'
    ELSE 'High'
END

-- Outlier Detection (IQR Method)
Q1 - 1.5*IQR < value < Q3 + 1.5*IQR

-- Power BI View
CREATE VIEW VW_SUPERSTORE_POWERBI AS (
    -- Shipping Days, Profit %, Profit Flag, all dimensions
)
```

### 🟢 Step 4 — Analytics Layer (30+ Queries)
- Business KPIs, segment analysis, time trends, statistical analysis, product deep-dive

---

## 📈 Key Performance Indicators (KPIs)

| KPI | Value | Interpretation |
|-----|-------|----------------|
| 💰 Total Sales | **$12.63M** | 4-year global revenue |
| 📈 Total Profit | **$1.46M** | Net profit |
| 📊 Profit Margin | **11.60%** | Overall margin |
| 🛒 Total Orders | **25,035** | Unique orders |
| 👥 Customers | **4,873** | Unique buyers |
| 📦 Products | **10,292** | Product catalog |
| 📈 YoY Growth | **90%** | 2011 → 2014 |

---

## 🔍 Deep-Dive Insights

### 1️⃣ Segment Analysis

| Segment | Sales | Profit | Margin | Share |
|---------|-------|--------|--------|-------|
| 👤 Consumer | $6.50M | $746,959 | 11.49% | **51.5%** |
| 🏢 Corporate | $3.82M | $440,964 | 11.53% | 30.2% |
| 🏠 Home Office | $2.31M | $276,709 | 11.99% | 18.3% |

> 💡 **Insight:** **Consumer drives 51.5% of revenue.** Home Office has the best margin (11.99%) but smallest volume.

---

### 2️⃣ Category Analysis — Furniture Problem

| Category | Sales | Profit | Margin |
|----------|-------|--------|--------|
| 💻 Technology | $4.74M | $662,293 | **13.97%** |
| 📎 Office Supplies | $3.78M | $517,222 | **13.68%** |
| 🪑 Furniture | $4.11M | $285,116 | **6.94%** ⚠️ |

> ⚠️ **ALERT:** Furniture has **high sales ($4.11M) but terrible margin (6.94%)** — nearly half of Technology/Office Supplies. Requires immediate cost optimization.

---

### 3️⃣ Year-over-Year Growth — Consistent 90% Growth

| Year | Sales | Profit | Orders | YoY Sales Growth |
|------|-------|--------|--------|------------------|
| 2011 | $2.26M | $247,655 | 4,440 | — |
| 2012 | $2.67M | $306,669 | 5,343 | +18% |
| 2013 | $3.40M | $406,478 | 6,721 | +27% |
| 2014 | $4.30M | $503,831 | 8,531 | +26% |

> 💡 **Insight:** Sales **nearly doubled** from 2011 ($2.26M) to 2014 ($4.30M) — consistent ~20-27% YoY growth. Profit grew even faster (+103%).

---

### 4️⃣ Regional Performance — Global Variance

| Region | Sales | Margin | Notes |
|--------|-------|--------|-------|
| 🌍 Central | $2.82M | 11.03% | Highest volume |
| 🌍 South | $1.60M | 8.76% | Below average margin |
| 🌍 North | $1.24M | **15.60%** | High efficiency |
| 🌏 North Asia | $848K | **19.52%** | Best non-Canada margin |
| 🇨🇦 Canada | $67K | **26.62%** | Highest margin (low volume) |
| 🌏 Southeast Asia | — | **1.99%** ⚠️ | Weakest region |

> ⚠️ **Southeast Asia has only 1.99% margin** — evaluate if this market is worth continued investment.

---

### 5️⃣ Product Analysis — Winners & Losers

**🏆 Top Profitable Products:**

| Product | Profit |
|---------|--------|
| Canon Imageclass Copier | **$25,200** |
| Cisco Smart Phone | $17,239 |

**💀 Biggest Loss Makers:**

| Product | Loss |
|---------|------|
| Cubify 3D Printer | **-$8,880** |
| Lexmark Printer | -$4,590 |

> 💡 **Recommendation:** Discontinue 3D Printers immediately — consistent loss makers across all markets.

---

### 6️⃣ Shipping Analysis

| Ship Mode | Orders | Sales | Share |
|-----------|--------|-------|-------|
| 📦 Standard Class | 30,749 | $7.57M | **60%** |
| 📬 Second Class | 10,302 | $2.56M | 20% |
| ✈️ First Class | 7,502 | $1.83M | 15% |
| ⚡ Same Day | 2,699 | $667K | 5% |

> 💡 **Insight:** **60% of orders use Standard shipping.** Same Day is only 5% — potential premium service opportunity.

---

### 7️⃣ Statistical Analysis — Outlier Detection

| Metric | Mean | Std Dev | Outliers (%) | Method |
|--------|------|---------|-------------|--------|
| Profit | — | — | **19.03%** | IQR |
| Shipping Cost | — | — | **11.52%** | IQR |
| Sales | — | — | — | IQR |

> ⚠️ **19% of profit values are outliers** — driven by heavy discounting. This significantly impacts overall margin calculations.

---

### 8️⃣ Sales Per Unit (SPU) Analysis

| Dimension | Highest SPU | Lowest SPU |
|-----------|-------------|------------|
| Category | Technology | Office Supplies |
| Segment | Home Office | Consumer |
| Discount Band | No Discount | High Discount |

> 💡 **Insight:** SPU drops dramatically with higher discounts — confirming that heavy discounting destroys per-unit value.

---

### 9️⃣ Power BI View — Business Intelligence Layer

```sql
CREATE VIEW VW_SUPERSTORE_POWERBI AS
SELECT *,
    DATEDIFF(DAY, ORDER_DATE, SHIP_DATE) AS SHIPPING_DAYS,
    ROUND(PROFIT / SALES * 100, 2) AS PROFIT_PERCENT,
    CASE WHEN PROFIT > 0 THEN 'Profit' ELSE 'Loss' END AS PROFIT_FLAG
FROM SUPERSTORE_CLEAN;
```

> Ready for Power BI / Tableau / Streamlit dashboard connection.

---

## 📋 Complete Analysis Catalog (9 Sections, 30+ Queries)

| Section | # | Analysis | Layer |
|---------|---|----------|-------|
| **Part 1: Data Cleaning** | 1 | Date format conversion (VARCHAR → DATE) | Silver |
| | 2 | Encoding fix in product names (278 rows) | Silver |
| | 3 | Duplicate removal (38 duplicates) | Silver |
| | 4 | Market column standardization | Silver |
| | 5 | Whitespace trimming on all text columns | Silver |
| **Part 2: Business KPIs** | 6 | Sales, Profit, Margin, Orders, Customers | Analytics |
| | 7 | Null/data quality checks | Silver |
| **Part 3: Segment/Category/Region** | 8 | Segment-wise sales & profit | Analytics |
| | 9 | Category-wise performance | Analytics |
| | 10 | Region-wise analysis | Analytics |
| **Part 4: Time Analysis** | 11 | Year-over-year sales trend | Analytics |
| | 12 | Monthly/quarterly patterns | Analytics |
| **Part 5: Product Analysis** | 13 | Top profitable products | Analytics |
| | 14 | Biggest loss-making products | Analytics |
| | 15 | Sub-category profitability | Analytics |
| **Part 6: Shipping & Discount** | 16 | Ship mode distribution | Analytics |
| | 17 | Discount impact on profit | Analytics |
| **Part 7: Statistical Analysis** | 18 | Descriptive stats (Mean, Std, Percentiles) | Gold |
| | 19 | Skewness & Kurtosis | Gold |
| | 20 | Outlier detection (IQR method) | Gold |
| **Part 8: SPU Analysis** | 21 | SPU by Category | Gold |
| | 22 | SPU by Sub-Category | Gold |
| | 23 | SPU by Segment | Gold |
| | 24 | SPU by Discount Band | Gold |
| | 25 | SPU Yearly Trend | Gold |
| **Part 9: Power BI View** | 26 | VW_SUPERSTORE_POWERBI creation | Gold |

---

## 🛠️ SQL Techniques & Methods

| Technique | Use Case |
|-----------|----------|
| `TO_DATE(col, 'DD-MM-YYYY')` | Date type conversion |
| `REPLACE() / TRIM()` | Encoding fix & whitespace cleanup |
| `ROW_NUMBER() OVER()` | Duplicate detection & removal |
| `PERCENTILE_CONT(0.25/0.75)` | IQR calculation for outliers |
| `STDDEV() / AVG()` | Descriptive statistics |
| `SKEW() / KURTOSIS()` | Distribution shape analysis |
| `SUM() / COUNT() / ROUND()` | KPI aggregations |
| `CASE WHEN` | Discount bands, profit flags |
| `CREATE VIEW` | BI-ready analytical layer |
| `GROUP BY ROLLUP` | Multi-level aggregations |
| `DATEDIFF()` | Shipping days calculation |
| `RATIO_TO_REPORT()` | Percentage share calculations |

---

## ✅ Key Findings & Recommendations

| # | Finding | Recommendation | Priority |
|---|---------|----------------|----------|
| 1 | Furniture: 6.94% margin (half of others) | Renegotiate supplier costs, reduce discounts on furniture | 🔴 High |
| 2 | 3D Printers: -$8,880 loss | Discontinue immediately — consistent loss maker | 🔴 High |
| 3 | 19% profit values are outliers (discounting) | Cap maximum discount at 30%; review approval process | 🔴 High |
| 4 | Southeast Asia: 1.99% margin | Evaluate market exit or restructure pricing strategy | 🟡 Medium |
| 5 | 90% sales growth (2011→2014) | Accelerate investment in Technology & Office Supplies | 🟡 Medium |
| 6 | Consumer = 51.5% of revenue | Invest in consumer loyalty programs & personalization | 🟡 Medium |
| 7 | Standard shipping = 60% | Offer premium shipping incentives to increase AOV | 🟢 Low |
| 8 | Canada: 26.62% margin (highest) | Explore expansion in high-margin, low-volume markets | 🟢 Low |
| 9 | Same Day shipping only 5% | Premium positioning opportunity for urgent orders | 🟢 Low |

---

## 🖥️ Tech Stack

| Layer | Technology |
|-------|------------|
| **Cloud Platform** | Snowflake |
| **Compute** | COMPUTE_WH (Virtual Warehouse) |
| **Database** | Superstore Dataset |
| **Language** | SQL |
| **Role** | ACCOUNTADMIN |
| **IDE** | Snowsight (Snowflake Web UI) |
| **BI Tool** | Power BI (via VW_SUPERSTORE_POWERBI) |

---

## 🚀 How to Run

```sql
-- Step 1: Set context
USE DATABASE <your_database>;
USE SCHEMA PUBLIC;

-- Step 2: Verify data
SELECT * FROM SUPERSTORE LIMIT 10;

-- Step 3: Run superstore_queries.sql sections sequentially


## 👤 Author

**Saswat Betta Aptakam**

---

*Built with ❄️ Snowflake | End-to-End Data Engineering Project*
