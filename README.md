🏡 Real-Estate-Business-Aalysis — Power BI Dashboard

Analyzes housing market data to uncover insights on pricing trends, housing characteristics, sales demand, and valuation gaps. Highlights KPIs such as SQM pricing, median sales change, offer-to-purchase ratios, and last 12-month sales. Enables comparison by house type, sales type, and time period.

🔗 Live Link : https://app.powerbi.com/links/B4dO9-ubut?ctid=e0d6db51-483a-41a8-bc9f-57219bf8811f&pbi_source=linkShare&bookmarkGuid=60a7e812-827b-4978-9b5d-b049e22853a4

🧰 Technologies Used

  📊 Power BI (Dashboarding & Visualization)
  🧮 DAX (KPIs & Calculations)
  🔍 SQL (Querying & Data Extraction)
  ☁️ Google BigQuery (Data Warehouse + Data Source)
  🔁 Power Query (Data Cleaning & Transformation)
  🗄️ Data Modeling & Relationship Design

  🧾 KPIs & Insights
        Key performance indicators calculated:
        Median Sales Price Change
        SQM Price (Avg)
        Offer vs Purchase Ratio
        Last 12-Month Sales
        Property Age (Years)

#Dashboards enable insights like:
✔ Pricing patterns across quarters
✔ New vs Resale home comparison
✔ Value differences by house type
✔ Negotiation and valuation gaps
✔ Sales seasonality & market demand

🎯 Target Users
      Investors
      Buyers
      Real Estate Analysts
      Market Research Teams

🚀 Outcome
    Provides a data-driven market intelligence dashboard combining cloud warehousing, SQL transformations, and BI modeling for decision-making.

🎯 Business Purpose

  Helps real estate analysts, investors, financial planners, and buyers evaluate:
  Pricing trends
  Housing valuation
  Demand cycles
  Negotiation leverage
  Property performance across time

  📐 DAX Calculations
  Age = ABS(YEAR(Housing[date].[Date]) - Housing[year_build] )
Offer Price = (100*Housing[purchase_price])/(100-Housing[%_change_between_offer_and_purchase]) 
Average Price SQM = AVERAGE(Housing[sqm_price]) 
Last 12 Month Sales = CALCULATE(SUM(Housing[purchase_price]),DATESINPERIOD(Housing[date],MAX(Housing[date]),-12,MONTH)) 
"Median Sales Price Change = 
 Var CurrMedianPrice = 
        MEDIANX(FILTER(Housing,
        YEAR(Housing[date].[Date])=
        YEAR(MAX(Housing[date].[Date]))),
        Housing[purchase_price])

Var PreMedianPrice = 
        MEDIANX(FILTER(Housing,YEAR(Housing[date].[Date])=YEAR(MAX(Housing[date].[Date]))-1),Housing[purchase_price])

RETURN
    IF(PreMedianPrice<>0, (CurrMedianPrice-PreMedianPrice)/PreMedianPrice,
    BLANK())"
Offer to SQM Ration = DIVIDE(SUM(Housing[Offer Price]),SUM(Housing[sqm])) 
"Sales by Region = 
    CALCULATE(SUM(Housing[purchase_price]),ALLEXCEPT(Housing,Housing[region]))"
TotalYTD Sales = TOTALYTD(SUM(Housing[purchase_price]),Housing[date].[Date]) 
"Units sold in latest Year & Quarter = 
        CALCULATE(DISTINCTCOUNT(Housing[house_id]),
        YEAR(Housing[date])= YEAR(MAX(Housing[date])) && QUARTER(Housing[date ])=QUARTER(MAX(Housing[date])))"
"YOY_Sales_Growth = 
 Var CurrYearSales =
        CALCULATE(SUM(Housing[purchase_price]),
                 YEAR(Housing[date (MM/DD/YYYY)])=YEAR(max(Housing[date])))
            
Var Prevyearsales =
        CALCULATE(SUM(Housing[purchase_price]),
        YEAR(Housing[date])=year(max(Housing[date]))-1)
Return
    IF(Prevyearsales<>0, (CurrYearSales-Prevyearsales)/Prevyearsales,BLANK())"
<img width="1039" height="1579" alt="image" src="https://github.com/user-attachments/assets/1ae0680d-34b6-4d43-a945-8c68cd9e0c0c" />
