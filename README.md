# Power-BI-Healthcare-Analysis
Hospital Monitoring Dashboard

Interactive Dashboard

 ### 1. Domain: Healthcare Analytics

# Analysis Details
 ## i. Business Case
 
🚩 Problem Statement:

The E-Commerce Sales Analytics Dashboard aims to address several key business challenges related to sales performance, customer behavior, product profitability, and regional growth. Despite generating strong revenue and profit, the organization faces gaps in customer retention, uneven regional performance, and product return issues that impact overall business efficiency. To support data-driven decision-making, the project focuses on identifying underlying issues and converting raw transactional data into meaningful insights.

The primary business problems addressed in this project include:

✔️ Declining revenue per customer at the start of each month, indicating potential behavioral or promotional timing gaps.

✔️ High return rates in specific product categories, especially Shorts, which negatively impact profit margins and customer satisfaction.

✔️ Regional sales imbalance, with North America outperforming other regions, highlighting untapped market potential in Europe, Asia-Pacific, and South America.

✔️ Dependence on a small group of high-performing products, increasing risk if demand shifts.

✔️ Suboptimal customer retention, where many customers fall into “Potential Loyalists” or “At-Risk” segments instead of moving into loyal or champion categories.

✔️ Insufficient demographic targeting, as the business lacks actionable insights into how age, gender, and marital status influence purchase behavior.

✔️ Inefficient forecasting and inventory allocation, causing fluctuations in demand planning.

This project provides a structured analytical approach to uncover these issues and enables the business to make informed decisions regarding pricing, product strategy, customer engagement, and market expansion.

 ## ii. Snapshots


 ## iii. Dashboard Features

                             Dynamic Features:
                                              1. Tooltips : Matrix in Line Chart
                                              2. Drill Through : Table Chart with Gauge Charts
                                              3. Drill Down : Stacked Bar Charts
                                              4. Filed Parameter : Sales Metrics                  
                             Analytical Features:
                                              1. KPI Cards : Total Orders, Total Revenue, Net Profit, Profit Margin and Rate of Return
                                              2. Stacked Bard Chart: Number of Orders by Category and Sub Category
                                              3. Line Charts : Trend and Forecasting, Net Profit Vs Adjusted Profit
                                              4. Table chart : Top 10 Products by Profit, Sales by Continents/Country/Regions
                                              5. Gauge Charts : Tagrgets VS Profit/Order/Revenue
                                              6. Map : Country by Total Revenue
                                              7. Pie Charts : Customers' Demographic Analyses
                                              8. Matrix : Customer Segmentation
                                              
 ## iv. Insights and Recommendations

                 Summary Insights
                        1. The business has achieved 25K total orders within the selected period.
                        2. Total revenue is 25M, showing strong overall sales performance.
                        3. Net profit is 10M, resulting in an excellent 42% profit margin.
                        4. The return rate is 2.2%, indicating efficient operations and product quality.
                        5. The forecasting chart shows a clear upward trend, meaning revenue is expected to grow steadily.
                        6. “Tires and Tubes” is the most ordered product sub-category.
                        7. “Shorts” is the sub-category with the highest return rate.
                        8. “Bib-Shorts” is the top-performing product in terms of revenue and net profit.
                        9. The top 10 products by profit show that cycling gear dominates the highest revenue list.
                       10. There are 18,148 total customers, and 17,416 have made purchases, giving a strong customer purchase rate.
                       11. The average revenue per customer is approximately $1,430.
                       12. Gender distribution is nearly balanced, with slightly more male customers.
                       13. Most customers fall within the 25–34 age group, indicating a young target audience.
                       14. The customer segmentation (RFM) shows a large portion in the “Potential Loyalists” and “Champions” categories.
                       15. Revenue per customer has a declining trend at the start of the month but stabilizes later.
                       16. Single customers represent the majority of buyers, which may influence product preferences.
                       17. North America generates the highest total revenue and profit, with 42.5% profit margin.
                       18. Europe, although significant in sales volume, shows slightly lower return rates compared to NA.
                       19. Revenue is widely diversified across continents, reducing business risk.
                       20. The United States leads all countries in both revenue and total orders, followed by the U.K. and Germany.

                Recommendations for Business Growth
                       1. Focus Marketing on High-Performing Segments. It is recommended to target promotions to “Champions” and “Potential Loyalists” to maximize repeat purchases.
                       2. Improve Product Quality for High-Return Categories. It is necessary to investigate Shorts category (highest return rate) for sizing, material, or expectation mismatch issues.
                       3. Expand Inventory & Promotions for High-Demand Products. The company can increase advertising and stock for Tires and Tubes, Bib-Shorts, and other top-profit items.
                       4. Grow Underperforming Regions With High Potential. Europe and Asia-Pacific show significant order volume—launch region-specific campaigns and pricing adjustments.
                       5. Enhance Customer Lifetime Value. The company can introduce loyalty programs for young customers (25–34 age group), who represent the highest engagement segment.
 ## v. Data Source
 
 ## vi. Dashboard Theme:
 JSON File

# A - Analysis Techniques:
# A1 - Data Preparation (Power Query & Normalization)

## A1.0 Power Query

### A1.1 Data Cleaning



### A1.2 Data Transformation

![Healthcare Fact Table Transformation](https://github.com/Morsshed/Power-BI-Healthcare-Analysis/blob/main/Healthcare%20Fact%20Table%20Transformation.png?raw=true)


### A1.3 Data Normalization

![Healthcare Data Normalisation Diagram](https://github.com/Morsshed/Power-BI-Healthcare-Analysis/blob/main/Healthcare%20Data%20Normalisation.png?raw=true)


# A2 - Fact Vs Dimentaion Tables (Relationship)

                                         Fact Table:
                                               1. HealthStatData
                                         Dimension Tables:
                                               1. Dim Condition
                                               2. Dim Date
                                           

  ## A2.1 - Data Model

![Healthcare Data Model Diagram](https://github.com/Morsshed/Power-BI-Healthcare-Analysis/blob/main/Healthcare%20Data%20Model.png?raw=true)
  
  ## A2.2 - Cardinality

![Healthcare Data Relationship Diagram](https://github.com/Morsshed/Power-BI-Healthcare-Analysis/blob/main/Healthcare%20Data%20Relationship.png?raw=true)


  ## A2.3 - Filter Direction
  
![Healthcare Data Cross-Filter Diagram](https://github.com/Morsshed/Power-BI-Healthcare-Analysis/blob/main/Healthcare%20Data%20Cross%20Filter.png?raw=true)


# B - DAX Languages

 ## B1.1 - Calculated Tables

   ### B.1.2 Lookup Date Table
   
       let
          Source = {Number.From(List.Min(FactSales[OrderDate]))..Number.From(List.Max(FactSales[OrderDate]))},
          #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
          #"Changed Type" = Table.TransformColumnTypes(#"Converted to Table",{{"Column1", type date}}),
          #"Renamed Columns" = Table.RenameColumns(#"Changed Type",{{"Column1", "Date"}}),
          #"Inserted Year" = Table.AddColumn(#"Renamed Columns", "Year", each Date.Year([Date]), Int64.Type),
          #"Inserted Quarter" = Table.AddColumn(#"Inserted Year", "Quarter", each Date.QuarterOfYear([Date]), Int64.Type),
          #"Inserted Month" = Table.AddColumn(#"Inserted Quarter", "Month", each Date.Month([Date]), Int64.Type),
          #"Inserted Month Name" = Table.AddColumn(#"Inserted Month", "Month Name", each Date.MonthName([Date]), type text),
          #"Inserted Start of Month" = Table.AddColumn(#"Inserted Month Name", "Start of Month", each Date.StartOfMonth([Date]), type date),
          #"Inserted Week of Year" = Table.AddColumn(#"Inserted Start of Month", "Week of Year", each Date.WeekOfYear([Date]), Int64.Type),
          #"Inserted Week of Month" = Table.AddColumn(#"Inserted Week of Year", "Week of Month", each Date.WeekOfMonth([Date]), Int64.Type),
          #"Inserted Day Name" = Table.AddColumn(#"Inserted Week of Month", "Day Name", each Date.DayOfWeekName([Date]), type text),
          #"Added Conditional Column" = Table.AddColumn(#"Inserted Day Name", "Day Type", each if [Day Name] = "Saturday" then "Weekend" else if [Day Name] = "Sunday" then "Weekend" else "Weekday"),
          #"Changed Type1" = Table.TransformColumnTypes(#"Added Conditional Column",{{"Day Type", type text}}),
          #"Extracted First Characters" = Table.TransformColumns(#"Changed Type1", {{"Month Name", each Text.Start(_, 3), type text}}),
          #"Added Prefix" = Table.TransformColumns(#"Extracted First Characters", {{"Quarter", each "Q" & Text.From(_, "en-US"), type text}}),
          #"Inserted Merged Column" = Table.AddColumn(#"Added Prefix", "Year-Quarter", each Text.Combine({Text.From([Year], "en-US"), [Quarter]}, "-"), type text),
          #"Reordered Columns" = Table.ReorderColumns(#"Inserted Merged Column",{"Date", "Year", "Quarter", "Year-Quarter", "Month", "Month Name", "Start of Month", "Week of Year", "Week of Month", "Day Name", "Day Type"}),
          #"Inserted Last Characters" = Table.AddColumn(#"Reordered Columns", "Last Characters", each Text.End(Text.From([Year], "en-US"), 2), type text),
          #"Renamed Columns1" = Table.RenameColumns(#"Inserted Last Characters",{{"Last Characters", "Short Year"}}),
          #"Inserted Merged Column1" = Table.AddColumn(#"Renamed Columns1", "Mon-Year", each Text.Combine({[Month Name], [Short Year]}, "-"), type text),
          #"Reordered Columns1" = Table.ReorderColumns(#"Inserted Merged Column1",{"Date", "Start of Month", "Year", "Quarter", "Year-Quarter", "Month", "Month Name", "Week of Year", "Week of Month", "Day Name", "Day Type", "Short Year", "Mon-Year"}),
          #"Renamed Columns2" = Table.RenameColumns(#"Reordered Columns1",{{"Start of Month", "Start of the Month"}}),
          #"Inserted Day of Week" = Table.AddColumn(#"Renamed Columns2", "Day of Week", each Date.DayOfWeek([Date]), Int64.Type),
          #"Removed Columns" = Table.RemoveColumns(#"Inserted Day of Week",{"Day of Week"})
      in
          #"Removed Columns"
 
 ## B1.3 - Calculated Columns

                                   LOS Groups (Modified) = 
                                   SWITCH(
                                       TRUE(),
                                       HealthStatData[LOS (days)] <= 3, "Short Stay (0-3d)",
                                       HealthStatData[LOS (days)] <= 7, "Moderate Stay (4-7d)",
                                       HealthStatData[LOS (days)] <= 14, "Long Stay (8-14d)",
                                       "Extended Stay (+15d)"
                                   ) 

 ## B1.4 - Calculated Measures 
 
  #### KPI Measures
  
                                   Admitted Patients = DISTINCTCOUNT(HealthStatData[Patient ID])
                                   AVG Age = AVERAGE(HealthStatData[Age])
                                   AVG Billing Amount = DIVIDE([Total Billing],[Admitted Patients],BLANK())
                                   AVG LOS = AVERAGE(HealthStatData[LOS (days)])
                                   Total Billing = SUM(HealthStatData[Billing Amount])
                                   Total Doctors = DISTINCTCOUNT(HealthStatData[Doctor])
                                   Total Rooms = DISTINCTCOUNT(HealthStatData[Room Number])
                           

   #### Test Results
   
                                    % of Abnormal Results = DIVIDE([Abnormal Results],[Admitted Patients All], BLANK())
                                    % of Inconclusive Results = DIVIDE([Inconclusive Results],[Admitted Patients All], BLANK())
                                    % of Normal Results = DIVIDE([Normal Results],[Admitted Patients All], BLANK())
                                    Abnormal Results = CALCULATE([Admitted Patients],HealthStatData[Test Results] = "Abnormal") + 0
                                    Admitted Patients All = CALCULATE([Admitted Patients],ALL((DimCondition[Medical Condition])))
                                    Inconclusive Results = CALCULATE([Admitted Patients],HealthStatData[Test Results] = "Inconclusive") + 0
                                    Normal Results = CALCULATE([Admitted Patients],HealthStatData[Test Results] = "Normal") + 0

   #### Time Intelligence 

                                    LY Admitted Patients = CALCULATE([Admitted Patients], DATEADD(DimDate[Date],-1,YEAR))


                                    Rooms YoY = 
                                    VAR SelectedYear = SELECTEDVALUE('DimDate'[Year])
                                    VAR PrevYear = 
                                        IF(NOT ISBLANK(SelectedYear),
                                            SelectedYear - 1,
                                            BLANK()
                                        )
                                    VAR PrevYearValue = 
                                        IF(NOT ISBLANK(PrevYear),
                                            CALCULATE([Total Rooms], YEAR('DimDate'[Date]) = PrevYear),
                                            BLANK()
                                        )
                                    VAR CurrentValue = [Total Rooms]
                                    VAR YoYChange = 
                                        IF(
                                            AND(NOT ISBLANK(CurrentValue), NOT ISBLANK(PrevYearValue)),
                                            DIVIDE(CurrentValue - PrevYearValue, PrevYearValue),
                                            BLANK()
                                        )
                                    RETURN
                                    IF(
                                        ISBLANK(SelectedYear),
                                        "No selection",
                                        IF(
                                            NOT ISBLANK(YoYChange),
                                            IF(YoYChange > 0, 
                                                "↑ " & FORMAT(YoYChange, "#.0%") & " Vs " & PrevYear,
                                                "↓ " & FORMAT(YoYChange, "#.0%") & " Vs " & PrevYear
                                            ),
                                            "No Data"
                                        )
                                    )
                                    

                                    Doctors YoY = 
                                    VAR SelectedYear = SELECTEDVALUE('DimDate'[Year])
                                    VAR PrevYear = 
                                        IF(NOT ISBLANK(SelectedYear),
                                            SelectedYear - 1,
                                            BLANK()
                                        )
                                    VAR PrevYearValue = 
                                        IF(NOT ISBLANK(PrevYear),
                                            CALCULATE([Total Doctors], YEAR('DimDate'[Date]) = PrevYear),
                                            BLANK()
                                        )
                                    VAR CurrentValue = [Total Doctors]
                                    VAR YoYChange = 
                                        IF(
                                            AND(NOT ISBLANK(CurrentValue), NOT ISBLANK(PrevYearValue)),
                                            DIVIDE(CurrentValue - PrevYearValue, PrevYearValue),
                                            BLANK()
                                        )
                                    RETURN
                                    IF(
                                        ISBLANK(SelectedYear),
                                        "No selection",
                                        IF(
                                            NOT ISBLANK(YoYChange),
                                            IF(YoYChange > 0, 
                                                "↑ " & FORMAT(YoYChange, "#.0%") & " Vs " & PrevYear,
                                                "↓ " & FORMAT(YoYChange, "#.0%") & " Vs " & PrevYear
                                            ),
                                            "No Data"
                                        )
                                    )
                                    
                                    Bill YoY = 
                                    VAR SelectedYear = SELECTEDVALUE('DimDate'[Year])
                                    VAR PrevYear = 
                                        IF(NOT ISBLANK(SelectedYear),
                                            SelectedYear - 1,
                                            BLANK()
                                        )
                                    VAR PrevYearValue = 
                                        IF(NOT ISBLANK(PrevYear),
                                            CALCULATE([Total Billing], YEAR('DimDate'[Date]) = PrevYear),
                                            BLANK()
                                        )
                                    VAR CurrentValue = [Total Billing]
                                    VAR YoYChange = 
                                        IF(
                                            AND(NOT ISBLANK(CurrentValue), NOT ISBLANK(PrevYearValue)),
                                            DIVIDE(CurrentValue - PrevYearValue, PrevYearValue),
                                            BLANK()
                                        )
                                    RETURN
                                    IF(
                                        ISBLANK(SelectedYear),
                                        "No selection",
                                        IF(
                                            NOT ISBLANK(YoYChange),
                                            IF(YoYChange > 0, 
                                                "↑ " & FORMAT(YoYChange, "#.0%") & " Vs " & PrevYear,
                                                "↓ " & FORMAT(YoYChange, "#.0%") & " Vs " & PrevYear
                                            ),
                                            "No Data"
                                        )
                                    )
                                    
                                    AVG LOS YoY = 
                                    VAR SelectedYear = SELECTEDVALUE('DimDate'[Year])
                                    VAR PrevYear = 
                                        IF(NOT ISBLANK(SelectedYear),
                                            SelectedYear - 1,
                                            BLANK()
                                        )
                                    VAR PrevYearValue = 
                                        IF(NOT ISBLANK(PrevYear),
                                            CALCULATE([AVG LOS], YEAR('DimDate'[Date]) = PrevYear),
                                            BLANK()
                                        )
                                    VAR CurrentValue = [AVG LOS]
                                    VAR YoYChange = 
                                        IF(
                                            AND(NOT ISBLANK(CurrentValue), NOT ISBLANK(PrevYearValue)),
                                            DIVIDE(CurrentValue - PrevYearValue, PrevYearValue),
                                            BLANK()
                                        )
                                    RETURN
                                    IF(
                                        ISBLANK(SelectedYear),
                                        "No selection",
                                        IF(
                                            NOT ISBLANK(YoYChange),
                                            IF(YoYChange > 0, 
                                                "↑ " & FORMAT(YoYChange, "#.0%") & " Vs " & PrevYear,
                                                "↓ " & FORMAT(YoYChange, "#.0%") & " Vs " & PrevYear
                                            ),
                                            "No Data"
                                        )
                                    )
                                    
                                    AVG Age YoY = 
                                    VAR SelectedYear = SELECTEDVALUE('DimDate'[Year])
                                    VAR PrevYear = 
                                        IF(NOT ISBLANK(SelectedYear),
                                            SelectedYear - 1,
                                            BLANK()
                                        )
                                    VAR PrevYearValue = 
                                        IF(NOT ISBLANK(PrevYear),
                                            CALCULATE([AVG Age], YEAR('DimDate'[Date]) = PrevYear),
                                            BLANK()
                                        )
                                    VAR CurrentValue = [AVG Age]
                                    VAR YoYChange = 
                                        IF(
                                            AND(NOT ISBLANK(CurrentValue), NOT ISBLANK(PrevYearValue)),
                                            DIVIDE(CurrentValue - PrevYearValue, PrevYearValue),
                                            BLANK()
                                        )
                                    RETURN
                                    IF(
                                        ISBLANK(SelectedYear),
                                        "No selection",
                                        IF(
                                            NOT ISBLANK(YoYChange),
                                            IF(YoYChange > 0, 
                                                "↑ " & FORMAT(YoYChange, "#.0%") & " Vs " & PrevYear,
                                                "↓ " & FORMAT(YoYChange, "#.0%") & " Vs " & PrevYear
                                            ),
                                            "No Data"
                                        )
                                    )
                                    
                                    Admission YoY = 
                                    VAR SelectedYear = SELECTEDVALUE('DimDate'[Year])
                                    VAR PrevYear = 
                                        IF(NOT ISBLANK(SelectedYear),
                                            SelectedYear - 1,
                                            BLANK()
                                        )
                                    VAR PrevYearValue = 
                                        IF(NOT ISBLANK(PrevYear),
                                            CALCULATE([Admitted Patients], YEAR('DimDate'[Date]) = PrevYear),
                                            BLANK()
                                        )
                                    VAR CurrentValue = [Admitted Patients]
                                    VAR YoYChange = 
                                        IF(
                                            AND(NOT ISBLANK(CurrentValue), NOT ISBLANK(PrevYearValue)),
                                            DIVIDE(CurrentValue - PrevYearValue, PrevYearValue),
                                            BLANK()
                                        )
                                    RETURN
                                    IF(
                                        ISBLANK(SelectedYear),
                                        "No selection",
                                        IF(
                                            NOT ISBLANK(YoYChange),
                                            IF(YoYChange > 0, 
                                                "↑ " & FORMAT(YoYChange, "#.0%") & " Vs " & PrevYear,
                                                "↓ " & FORMAT(YoYChange, "#.0%") & " Vs " & PrevYear
                                            ),
                                            "No Data"
                                        )
                                    )

   #### Time Intelligence 

                                   Order YTD = CALCULATE([# of Orders], DATESYTD(DimDate[Date]))
                                   PM Profit = CALCULATE([Net Profit], DATEADD(DimDate[Date],-1,MONTH))
                                   PM Quantity Returned = CALCULATE([Quantity Returned], DATEADD(DimDate[Date],-1,MONTH))
                                   PM Revenue = CALCULATE([Total Revenue], DATEADD(DimDate[Date],-1,MONTH) )
                                   PM Order = CALCULATE([# of Orders], DATEADD(DimDate[Date],-1,MONTH))

# C - Analyses and Interactivities:
  ## C1 - KPI and Domographic Analyses

  ## C2 - Trend Analyses

  ## C3 - Billing Analyses



# D. Conclusion
I truly enjoyed working on this project from beginning to end. Experiencing the full process provided valuable insights into both the data and the visuals. I look forward to tackling similar projects in the future and exploring even more complex datasets.
