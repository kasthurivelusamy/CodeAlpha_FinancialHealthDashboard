# CodeAlpha Task 1: Financial Health Dashboard

Power BI dashboard analysing the financial health of a small business (SME) using monthly data from Jan 2022 to Dec 2025.

## Objective
Visualize income statement, balance sheet and cash flow, analyse profitability trends over time, and support budgeting with forecast and budget vs actual.

## Tools
- Power BI Desktop (Power Query, DAX, data modelling)
- Excel (source data)

## Data
`data/Financials.xlsx` has 4 sheets (sample data created for this project):

| Sheet | Columns |
|---|---|
| IncomeStatement | Date, Revenue, COGS, OperatingExpenses, Interest, Tax |
| BalanceSheet | Date, CurrentAssets, FixedAssets, CurrentLiabilities, LongTermLiabilities, Equity, Inventory |
| CashFlow | Date, OperatingCF, InvestingCF, FinancingCF |
| Budget | Date, BudgetRevenue, BudgetExpense |

## Data model
A `Calendar` date table (DAX) is related one-to-many to the Date column of all 4 tables. See `dax/DAX_Measures.md` for the Calendar table and all measures.

## Report pages
1. **Overview**: KPI cards (Total Revenue, Net Profit, Net Margin %, Total Assets), revenue vs net profit trend, year slicer
2. **Income Statement**: net profit waterfall by year, gross / operating / net margin trends
3. **Balance Sheet**: Total Assets, Liabilities, Equity, Current Ratio, yearly comparison chart
4. **Cash Flow**: Operating, Investing, Financing and Net Cash Flow cards, cash flow by year, cumulative cash
5. **Forecast & Budget**: Budget vs Actual revenue, variance cards, revenue forecast (Power BI Analytics forecast)

## Key measures
Gross Profit, EBIT, Net Profit, Gross / Operating / Net Margin %, Current Ratio, Quick Ratio, Debt to Equity, ROE %, ROA %, Net Cash Flow, Cumulative Cash, Revenue YoY %, Net Profit YTD, Revenue Variance and Variance %.

## How to open
1. Download this repository
2. Open `CodeAlpha_FinancialHealthDashboard.pbix` in Power BI Desktop
3. If the data source path breaks: Home > Transform data > Data source settings > Change source, and point to `data/Financials.xlsx`

## Screenshots
See the `screenshots/` folder.

## Author
Submitted as part of the CodeAlpha Power BI internship.
