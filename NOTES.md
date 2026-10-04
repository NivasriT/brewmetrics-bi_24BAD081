# BrewMetrics BI - DAX Development & Copilot Log

### Measure 1: Sales MoM Growth %
**Prompt I gave Copilot:** "Write a DAX measure for Month over Month sales growth using Dim_Date"
**Copilot's first suggestion:**
Sales MoM Growth % = (SUM(Fact_Sales[sales_amount]) - CALCULATE(SUM(Fact_Sales[sales_amount]), DATEADD(Dim_Date[Date], -1, MONTH))) / CALCULATE(SUM(Fact_Sales[sales_amount]), DATEADD(Dim_Date[Date], -1, MONTH))
**What I changed and why:**
Copilot duplicated inline aggregations instead of using the `[Total Sales]` base measure and used direct division `/`. I refactored it to use `[Total Sales]` and `DIVIDE()` to handle division-by-zero safely.

### Measure 2: Running Total Sales
**Prompt I gave Copilot:** "Write a DAX measure for cumulative running total of total sales over time"
**Copilot's first suggestion:**
Running Total Sales = CALCULATE(SUM(Fact_Sales[sales_amount]), FILTER(ALL(Dim_Date), Dim_Date[Date] <= MAX(Dim_Date[Date])))
**What I changed and why:**
Copilot used `ALL(Dim_Date)`, which ignores active slicers on the page. I updated it to `ALLSELECTED(Dim_Date)` so filtering by city/product works as expected and referenced `[Total Sales]`.

### Measure 3: City Sales Rank
**Prompt I gave Copilot:** "Write a DAX measure using RANKX to rank cities by total sales"
**Copilot's first suggestion:**
City Sales Rank = RANKX(Dim_City, [Total Sales])
**What I changed and why:**
Copilot omitted `ALL(Dim_City[city])`, causing every city row in a visual to rank as 1 because it evaluated within its own filtered context. I added `ALL(Dim_City[city])` and set dense ranking.

### Measure 4: Average Basket Size
**Prompt I gave Copilot:** "Write a DAX measure for average sale value per transaction"
**Copilot's first suggestion:**
Average Basket Size = AVERAGE(Fact_Sales[sales_amount])
**What I changed and why:**
Copilot averaged row-level sales_amount, which calculates sales per line-item instead of per order basket. I changed it to divide `[Total Sales]` by `DISTINCTCOUNT(Fact_Sales[sale_id])`.