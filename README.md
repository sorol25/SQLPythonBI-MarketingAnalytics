<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d0d1a,40:1a0533,80:2d0a4e,100:6b21a8&height=220&section=header&text=Marketing%20Analytics&fontSize=40&fontColor=ffffff&fontAlignY=36&animation=fadeIn&desc=SQL%20%C3%97%20Python%20%C3%97%20Power%20BI%20%7C%BI%20Portfolio%20Project&descAlignY=56&descSize=15" width="100%"/>

<a href="https://git.io/typing-svg">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=20&pause=1000&color=a855f7&center=true&vCenter=true&width=780&lines=Customer+Journey+Analysis+%F0%9F%9B%A4%EF%B8%8F;Sentiment+Analysis+with+VADER+%F0%9F%A7%A0;Engagement+%26+Campaign+Performance+%F0%9F%93%A3;SQL+Data+Cleaning+%2B+Power+BI+Dashboard+%F0%9F%93%8A;From+Raw+Data+to+Marketing+Intelligence" alt="Typing SVG" />
</a>

<br/>

<p>
  <img src="https://img.shields.io/badge/SQL_Server-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white"/>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black"/>
  <img src="https://img.shields.io/badge/NLTK_VADER-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/DAX-F2C811?style=for-the-badge&logo=powerbi&logoColor=black"/>
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
</p>

<p>
  <img src="https://img.shields.io/github/stars/sorol25/SQLPythonBI_MarketingAnalytics?style=for-the-badge&color=a855f7"/>
  <img src="https://img.shields.io/github/forks/sorol25/SQLPythonBI_MarketingAnalytics?style=for-the-badge&color=7c3aed"/>
  <img src="https://img.shields.io/badge/License-MIT-22c55e?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-Complete-a855f7?style=for-the-badge"/>
</p>

</div>

---

## 📌 Project Overview

> **A full marketing intelligence pipeline** — from raw SQL tables and dirty review text, through Python-powered NLP sentiment enrichment, all the way to a Power BI dashboard that tells the full customer story.

This project answers the core questions every marketing team needs answered: *Who are our customers? Where do they drop off in their journey? What do they really think about us? Which campaigns and content actually drive engagement?*

---

## 🗺️ Project Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                        PIPELINE OVERVIEW                            │
├───────────────┬───────────────┬────────────────┬────────────────────┤
│  🗄️  SQL      │  🐍 PYTHON   │  📊 POWER BI   │  📝 PRESENTATION  │
│               │               │                │                    │
│  customers    │  Fetch reviews│  Import all    │  Problem           │
│  + geography  │  from SQL     │  cleaned data  │  Statements        │
│  JOIN         │               │                │                    │
│               │  VADER NLP    │  Calendar DAX  │  Dashboard         │
│  products     │  sentiment    │  table built   │  walkthrough       │
│  price tiers  │  scoring      │                │                    │
│               │               │  KPI tiles     │  Insight           │
│  customer     │  Categorize → │  Journey funnel│  narrative         │
│  journey      │  Positive     │  Engagement    │                    │
│  dedup + clean│  Mixed        │  Sentiment     │                    │
│               │  Negative     │  charts        │                    │
│  engagement   │  Neutral      │                │                    │
│  data clean   │               │  Drill-through │                    │
│               │  Export CSV   │  filters       │                    │
│  reviews clean│  ─────────────▶ load enriched  │                    │
└───────────────┴───────────────┴────────────────┴────────────────────┘
```

---

## 📁 Repository Structure

```
SQLPythonBI_MarketingAnalytics/
│
├    🗄️  SQL Queries
├── customers.sql                        # Customer + geography JOIN
├── products.sql                         # Product price-tier categorization
├── reviews.sql                          # Review text whitespace cleaning
├── fact_customer_journey.sql            # Journey deduplication + NULL imputation
├── fact_engagement_data.sql             # Engagement data normalization
│
├     🐍 Python
├── customer_reviews_enrichment.py       # VADER sentiment scoring + categorization
├── fact_customer_reviews_enrich.csv     # Output: enriched reviews with sentiment
│
├     📊 Power BI
├── Dashboard.pbix                       # Interactive marketing dashboard
├──  Calendar DAX Script.txt             # Custom DAX date table (2023–2025)
│
├    💾 Database
├──  PortfolioProject_MarketingAnalytics.bak  # SQL Server database backup
│
├    📝 Presentations
├── problem statements.pptx             # Business problem framing
├── PresentationSlide.pptx              # Final stakeholder presentation
│
└── 📖 README.md
```

---

## 🚀 Getting Started

### Prerequisites

```
SQL Server (Express or full)  |  Python 3.8+  |  Power BI Desktop
```

Install Python dependencies:

```bash
pip install pandas pyodbc nltk sqlalchemy
```

---

### Step 1 — Restore the Database

Open SQL Server Management Studio (SSMS) and restore the backup:

```sql
RESTORE DATABASE PortfolioProject_MarketingAnalytics
FROM DISK = 'path\to\PortfolioProject_MarketingAnalytics.bak'
WITH REPLACE;
```

---

### Step 2 — Run the SQL Cleaning Queries

Execute each `.sql` file against the restored database in this order:

| Order | File | Purpose |
|---|---|---|
| 1 | `customers.sql` | JOIN customers with geography to enrich with Country + City |
| 2 | `products.sql` | Add `PriceCategory` column: **Low** / **Medium** / **High** |
| 3 | `reviews.sql` | Strip double spaces from `ReviewText` with `REPLACE()` |
| 4 | `fact_customer_journey.sql` | Deduplicate journey records with `ROW_NUMBER()`, impute NULLs via `AVG() OVER()` |
| 5 | `fact_engagement_data.sql` | Normalize `ContentType`, split `ViewsClicksCombined`, reformat dates |

---

### Step 3 — Run Sentiment Enrichment (Python)

Update the connection string in `customer_reviews_enrichment.py`:

```python
conn_str = (
    "Driver={SQL Server};"
    "Server=YOUR_SERVER\\SQLEXPRESS;"          # <-- update this
    "Database=PortfolioProject_MarketingAnalytics;"
    "Trusted_Connection=yes;"
)
```

Then run:

```bash
python customer_reviews_enrichment.py
```

**Output:** `fact_customer_reviews_with_sentiment.csv` with three new columns:

| Column | Description |
|---|---|
| `SentimentScore` | VADER compound score: –1.0 (most negative) → +1.0 (most positive) |
| `SentimentCategory` | `Positive` · `Mixed Positive` · `Neutral` · `Mixed Negative` · `Negative` |
| `SentimentBucket` | Score range: `0.5 to 1.0` · `0.0 to 0.49` · `-0.49 to 0.0` · `-1.0 to -0.5` |

---

### Step 4 — Build the Power BI Dashboard

1. Open `Dashboard.pbix` in Power BI Desktop
2. Connect to your SQL Server database
3. Import `fact_customer_reviews_enrich.csv` for sentiment data
4. The Calendar table is already built via DAX — covering **2023–2025** with:

```dax
Calendar =
ADDCOLUMNS (
    CALENDAR ( DATE ( 2023, 1, 1 ), DATE ( 2025, 12, 31 ) ),
    "Year", YEAR ( [Date] ),
    "Quarter", "Q" & FORMAT ( [Date], "Q" ),
    "MonthNameShort", FORMAT ( [Date], "mmm" ),
    "DayOfWeek", FORMAT ( [Date], "dddd" )
    -- + 8 more time intelligence columns
)
```

---

### Step 5 — Review Problem Statements & Present

- 📋 Open `problem statements.pptx` to understand the business questions this project answers
- 🎯 Open `PresentationSlide.pptx` for the stakeholder-ready insight delivery

---

## 🔍 What the SQL Queries Do

### `customers.sql` — Geographic Enrichment

Joins `dbo.customers` with `dbo.geography` on `GeographyID` to attach **Country** and **City** to every customer record for geographic segmentation.

### `products.sql` — Price Tier Classification

```sql
CASE
    WHEN Price < 50       THEN 'Low'
    WHEN Price BETWEEN 50 AND 200 THEN 'Medium'
    ELSE                       'High'
END AS PriceCategory
```

Enables conversion rate analysis broken down by product price tier.

### `fact_customer_journey.sql` — Deduplication + Imputation

Uses a two-pass approach:
- **Pass 1:** `ROW_NUMBER() OVER(PARTITION BY CustomerID, ProductID, VisitDate, Stage, Action)` to tag duplicates
- **Pass 2:** `COALESCE(Duration, AVG(Duration) OVER(PARTITION BY VisitDate))` to fill NULL durations with the daily average
- `UPPER(Stage)` normalizes inconsistent casing across journey stages

### `fact_engagement_data.sql` — Content Normalization

```sql
UPPER(REPLACE(ContentType, 'Socialmedia', 'Social Media'))  -- fix & uppercase
LEFT(ViewsClicksCombined, CHARINDEX('-', ...) - 1)          -- extract Views
RIGHT(ViewsClicksCombined, LEN(...) - CHARINDEX('-', ...))  -- extract Clicks
FORMAT(CONVERT(DATE, EngagementDate), 'dd.MM.yyyy')         -- reformat date
```

Filters out `Newsletter` content type as out of scope for campaign analysis.

---

## 🧠 Sentiment Analysis — How It Works

The `customer_reviews_enrichment.py` script uses **NLTK VADER** (Valence Aware Dictionary and sEntiment Reasoner) — purpose-built for short, informal text like product reviews.

```python
# Dual-signal categorization: text sentiment + star rating
def categorize_sentiment(score, rating):
    if score > 0.05 and rating >= 4:   return 'Positive'
    if score > 0.05 and rating == 3:   return 'Mixed Positive'
    if score < -0.05 and rating <= 2:  return 'Negative'
    if score < -0.05 and rating == 3:  return 'Mixed Negative'
    # ... handles all edge cases between text and star signal
```

**Why dual-signal?** A 5-star review with negative language (sarcasm, backhanded compliments) and a 1-star review with positive words (apologetic, polite) both get correctly categorized — something pure star-rating analysis misses.

---

## 📊 Dashboard Coverage

The `Dashboard.pbix` file surfaces insights across four analytical areas:

```
📍 Customer Overview        — Demographics, geography, age/gender breakdown
🛤️  Customer Journey         — Funnel stages: Awareness → Consideration → Purchase
                              Drop-off rates, duration by stage, duplicate-clean data
📣 Engagement & Campaigns   — Views, clicks, likes by ContentType and CampaignID
                              Newsletter filtered; Social Media normalized
⭐ Sentiment Analysis        — Rating distribution, VADER score buckets,
                              Positive vs Mixed vs Negative breakdown over time
```

---

## 📜 License

```
MIT License — Copyright (c) 2026 Yeamine Alam Sorol
Free to fork, star, and build upon.
```

---

## 👨‍💻 About the Author

<div align="center">

**Yeamine Alam Sorol**
*Data Analyst · Full-Stack Developer · UI/UX Designer*

<br/>

<a href="https://www.linkedin.com/in/yeamine-alam-sorol-746831347">
  <img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white"/>
</a>
&nbsp;
<a href="https://github.com/sorol25">
  <img src="https://img.shields.io/badge/⭐_Star_This_Repo-181717?style=for-the-badge&logo=github&logoColor=white"/>
</a>

</div>

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:6b21a8,50:2d0a4e,100:0d0d1a&height=130&section=footer" width="100%"/>

<sub>If this project helped you, consider starring ⭐ the repo or sharing it with someone learning Data Analytics.</sub>

</div>
