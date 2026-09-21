📊 Superstore Sales Analysis
A business-focused analysis of Superstore retail sales data (Jan 2019 – Dec 2020), built with pandas and matplotlib to clean transactional records and identify where the business is losing money.
---
📁 Dataset
The raw file contains 5,901 order-line records across 23 columns, including Order ID, Order Date, Ship Date, Customer info, Segment, City, State, Region, Category, Sub-Category, Product Name, Sales, Quantity, Profit, Returns, and Payment Mode.
> The CSV itself is not included in this repo. To run the notebook, place `SuperStore_Sales_DataSet.csv` in the same folder as `Superstore-Sales-Analysis.ipynb` before running.
>
> Note: This dataset does **not** include a `Discount` field. Any statement about pricing or discounting below is explicitly ruled in/out based on evidence, not assumed.
---
🛠️ Project Workflow
Step 1: Loading Data — Loaded the raw CSV using `latin1` encoding.
Step 2: Data Audit — Checked shape, column names, data types, missing values, and duplicates. Found 5,901 rows, 0 duplicates, and 3 columns (`Returns`, `ind1`, `ind2`) with heavy or total missing values.
Step 3: Data Cleaning — Renamed a corrupted first column (`Row ID+O6G3A1:R6` → `Row ID`), dropped `Returns`, `ind1`, and `ind2` (mostly or entirely empty), converted `Order Date` to a proper datetime type, and stripped whitespace from column headers.
Step 4: Business Analysis — Grouped by Region, Category, Sub-Category, State, and City to compare sales against profit, and built a monthly sales trend.
Step 5: Root Cause Analysis — Investigated why certain cities show a net loss. Filtered out low-volume cities (fewer than 5 orders) to remove statistical noise, then identified which Sub-Category was driving the losses in the remaining cities.
Step 6: Visualization — Charted sales by region, profit by sub-category, top/bottom 5 states and cities, the monthly sales trend, and the root-cause breakdown.
---
🎯 Key Findings
Total performance: Across 5,901 orders, the business generated $1,565,804 in total sales and $175,262 in total profit.
Regional performance: The West region leads in sales ($522,441), followed by East, Central, and South.
Top product: The single highest-selling item is the 3D Systems Cube Printer, 2nd Generation, Magenta, generating $14,334.89 in sales.
Profit leaks by Sub-Category: Tables, Supplies, and Bookcases are the only sub-categories with a net loss overall — every other sub-category is profitable.
Geographic concentration: Losses are not spread evenly. Exactly 93 cities show a net loss, falling within 10 states whose total profit is negative overall (led by Texas), including Pennsylvania (Philadelphia) and Texas (Houston).
Signal vs. noise: Of the 93 loss-making cities, only 31 have meaningful order volume (5+ orders); the other 62 show a loss purely from 1–4 total orders, where a single bad transaction is enough to flip them negative.
---
🔍 Root Cause Analysis
Filtering the 93 loss-making cities down to the 31 with real order volume changes the story. Within those 31 cities, the biggest contributors to the loss are Binders and Machines — even though both Sub-Categories are profitable across the business overall. This means the loss isn't a company-wide pricing problem; it's something specific happening with these two product types in this particular set of cities.
---
💡 Conclusion & Final Recommendation
The losses are not a nationwide problem — they're concentrated in a narrow set of 31 cities, and driven almost entirely by two Sub-Categories (Binders and Machines) that are otherwise profitable everywhere else.
This dataset does not contain a `Discount` field, so discounting is ruled out as an explanation rather than assumed. The next step should be pulling the individual Binders and Machines transactions in these 31 cities to check whether the loss comes from a small number of high-value/bulk orders, high shipping or fulfillment cost, or another operational factor — not a blanket pricing fix.
---
💻 Tech Stack
Language: Python 3
Data Manipulation: pandas
Visualization: matplotlib
---
📌 Limitations
No `Discount` column exists in this dataset — pricing-related conclusions are intentionally ruled out with evidence rather than assumed.
"Loss-making" at the city level is filtered for order volume (5+ orders) specifically to avoid low-sample noise skewing the results.
