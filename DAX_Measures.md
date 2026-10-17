# DAX: Calendar table and measures

## Calendar table
```dax
Calendar =
ADDCOLUMNS (
    CALENDAR ( DATE ( 2022, 1, 1 ), DATE ( 2026, 12, 31 ) ),
    "Year", YEAR ( [Date] ),
    "Quarter", "Q" & QUARTER ( [Date] ),
    "MonthNo", MONTH ( [Date] ),
    "Month", FORMAT ( [Date], "MMM" ),
    "YearMonth", FORMAT ( [Date], "YYYY-MM" )
)
```
`Month` is sorted by `MonthNo`.

Calendar column used for the forecast chart:
```dax
MonthStart = DATE ( YEAR ( [Date] ), MONTH ( [Date] ), 1 )
```

## Income statement
```dax
Total Revenue = SUM ( IncomeStatement[Revenue] )
Total COGS = SUM ( IncomeStatement[COGS] )
Gross Profit = [Total Revenue] - [Total COGS]
Operating Expenses = SUM ( IncomeStatement[OperatingExpenses] )
EBIT = [Gross Profit] - [Operating Expenses]
Net Profit = [EBIT] - SUM ( IncomeStatement[Interest] ) - SUM ( IncomeStatement[Tax] )
Gross Margin % = DIVIDE ( [Gross Profit], [Total Revenue] )
Operating Margin % = DIVIDE ( [EBIT], [Total Revenue] )
Net Margin % = DIVIDE ( [Net Profit], [Total Revenue] )
```

## Balance sheet (point in time, last date of selected period)
```dax
Current Assets = CALCULATE ( SUM ( BalanceSheet[CurrentAssets] ), LASTDATE ( BalanceSheet[Date] ) )
Fixed Assets = CALCULATE ( SUM ( BalanceSheet[FixedAssets] ), LASTDATE ( BalanceSheet[Date] ) )
Current Liabilities = CALCULATE ( SUM ( BalanceSheet[CurrentLiabilities] ), LASTDATE ( BalanceSheet[Date] ) )
Long Term Liabilities = CALCULATE ( SUM ( BalanceSheet[LongTermLiabilities] ), LASTDATE ( BalanceSheet[Date] ) )
Total Equity = CALCULATE ( SUM ( BalanceSheet[Equity] ), LASTDATE ( BalanceSheet[Date] ) )
Inventory Value = CALCULATE ( SUM ( BalanceSheet[Inventory] ), LASTDATE ( BalanceSheet[Date] ) )
Total Assets = [Current Assets] + [Fixed Assets]
Total Liabilities = [Current Liabilities] + [Long Term Liabilities]
Current Ratio = DIVIDE ( [Current Assets], [Current Liabilities] )
Quick Ratio = DIVIDE ( [Current Assets] - [Inventory Value], [Current Liabilities] )
Debt to Equity = DIVIDE ( [Total Liabilities], [Total Equity] )
ROE % = DIVIDE ( [Net Profit], [Total Equity] )
ROA % = DIVIDE ( [Net Profit], [Total Assets] )
```

## Cash flow
```dax
Operating CF = SUM ( CashFlow[OperatingCF] )
Investing CF = SUM ( CashFlow[InvestingCF] )
Financing CF = SUM ( CashFlow[FinancingCF] )
Net Cash Flow = [Operating CF] + [Investing CF] + [Financing CF]
Cumulative Cash =
CALCULATE (
    [Net Cash Flow],
    FILTER ( ALL ( 'Calendar' ), 'Calendar'[Date] <= MAX ( 'Calendar'[Date] ) )
)
```

## Trend
```dax
Revenue LY = CALCULATE ( [Total Revenue], SAMEPERIODLASTYEAR ( 'Calendar'[Date] ) )
Revenue YoY % = DIVIDE ( [Total Revenue] - [Revenue LY], [Revenue LY] )
Net Profit YTD = TOTALYTD ( [Net Profit], 'Calendar'[Date] )
```

## Budget
```dax
Budget Revenue = SUM ( Budget[BudgetRevenue] )
Revenue Variance = [Total Revenue] - [Budget Revenue]
Revenue Variance % = DIVIDE ( [Revenue Variance], [Budget Revenue] )
```
