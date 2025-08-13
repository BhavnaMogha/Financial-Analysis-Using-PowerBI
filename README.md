Financial-Analysis-Using-PowerBI
Using PowerBI, Excel

📊 Financial Analysis – Power BI Project

🛠 Step 1: ETL Tasks (Power Query)
- 🗑 **Remove Unnecessary Columns** – Delete columns not useful for analysis.
- 🔢 **Data Type Correction** – Ensure numeric & date columns have correct types.
- 🔍 **Filter Data** – Keep only records for years **after 2014**.
- ➕ **Create New Column** – `Profit = Revenue - Expenses` (if applicable).
- ✏ **Rename Columns** – Use clear, user-friendly names.


🗂 Step 2: Data Modeling
- 📋 **Identify Fact & Dimension Columns**  
  - **Facts:** Revenue, Profit  
  - **Dimensions:** Country, Segment
- 📅 **Create Date Table** – Use DAX & link to main data table.
- 🔗 **Create Relationships** – Connect tables (Products, Regions, etc.) using proper keys.


📈 Step 3: Visualizations
- 📊 **Bar Chart** – Total Revenue by Country.
- 📉 **Line Chart** – Revenue Trend Over Time.
- 🏗 **Stacked Column Chart** – Revenue by Product & Year.
- 🌳 **Tree Map** – Profit by Segment.
- 🎚 **Slicers** – Year & Region filters.


🧮 Step 4: DAX Measures
- 💰 **Total Revenue**  
```DAX
Total Revenue = SUM(Financials[Revenue])
```
- 📊 **Profit Margin**  
```DAX
Profit Margin = DIVIDE(SUM(Financials[Profit]), SUM(Financials[Revenue]))
```
- 📆 **YoY Revenue Growth**  
```DAX
YoY Revenue Growth =
VAR CurrentRevenue = SUM(Financials[Revenue])
VAR LastYearRevenue =
    CALCULATE(SUM(Financials[Revenue]), SAMEPERIODLASTYEAR('Date'[Date]))
RETURN DIVIDE(CurrentRevenue - LastYearRevenue, LastYearRevenue)
```
- 🏆 **Top 5 Countries by Profit** – Use `TOPN` in DAX + visualization.
- 🔄 **Running Total Revenue**  
```DAX
Running Total Revenue =
CALCULATE(
    SUM(Financials[Revenue]),
    FILTER(
        ALLSELECTED('Date'),
        'Date'[Date] <= MAX('Date'[Date])
    )
)


🎯 Bonus Scenario
- ❓ **Business Question** – Which **customer segment + country** combinations have the highest YoY revenue growth?  
- 📊 **Solution** – Create a **matrix table**:  
  - Rows = Segments  
  - Columns = Countries  
  - Values = YoY Revenue Growth  
- 🎨 Apply **conditional formatting** to highlight top performers.
