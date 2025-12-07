# Power-BI-Healthcare-Analysis
Hospital Monitoring Dashboard
[View the Healthcare Analysis Dashboard](https://app.powerbi.com/view?r=eyJrIjoiOGMzNDA0NTYtZTRhNy00YTg4LWJlYWYtMzM2MjAxYjE2Y2YzIiwidCI6IjFhOTM4M2ZmLTVlMDEtNDkzYy04MTJmLTg0ODAzZTliMGI3YiJ9)

 ### 1. Domain: Healthcare Analytics

# Analysis Details
 ## i. Business Case
 
### Business Problem Statement

The company is experiencing a diversified customer purchase pattern where only a small group of high-value customers consistently contribute to revenue, while a majority remain in early-engagement stages such as Promising or Potential Loyalists. Although total revenue performance is stable, customer purchase frequency shows signs of fluctuation, and several customer segments are at risk of churn due to declining recency in their purchase behavior. To sustain growth, the business needs an effective segmentation-driven strategy to enhance customer retention, increase repeat purchase behavior, and convert mid-tier customers into top-value champions.

### Key Issues Identified

► Revenue is heavily dependent on a limited high-value customer segment (Champions & Loyal Customers).

► Large customer share falls in Promising or Potential Loyalist categories, indicating untapped lifetime value.

► Noticeable drop in purchase volume during certain periods despite revenue per customer remaining stable.

► Several customers show high recency value (haven’t purchased recently), signaling early churn.

► Professional occupation group dominates revenue contribution — reliance on one segment poses risk.

► Lower purchasing frequency among high spenders suggests lack of loyalty reinforcement.

► Slow conversion rate of low-value groups into loyal customers affects long-term growth potential.

### Business Objectives

○ Increase recurrent purchases by designing retention and engagement strategies.

○ Convert mid-tier customers into loyal and champion segments.

○ Recover inactive or slipping customers via targeted win-back campaigns.

○ Reduce dependency on a single high-revenue demographic.

○ Improve customer lifetime value through RFM-driven personalization.

○ Track customer movement between RFM segments over time for continuous optimization.

 ## ii. Snapshots

![Healthcare Analysis Overview](https://github.com/Morsshed/Power-BI-Healthcare-Analysis/blob/main/Healthcare%20Analysis.jpeg?raw=true)

 ## iii. Dashboard Features

                             Dynamic Features:
                                              1. Slicers : Year, Month, Medical Condistion, Hospital Name
                                              2. Page Nevigators : Demographis Analysis, Trend Analysis, Billing Analysis
                                              3. Live Image URL : Stacked Bar Charts
                                              4. Filed Parameter : Age Group, LOS (Length of Stay) Groups, Admission Type
                                              5. Numeric Parameter : Patients, AVG Age, AVG Billing 
                             Analytical Features:
                                              1. KPI Cards : Admitted Patients, Total Rooms, Total Billing, LY Admitted Patients
                                                             AVG LOS (Days), Patients AVG Age, Total Doctors,
                                              2. Card : LIVE Condition Description, LIVE Disease Image, Test Results
                                              3. Clustered Column Chart : Patient Types Parameters VS KPI Parameters
                                              4. Line chart : Month VS KPI Parameters
                                              5. Stacked Column Chart : Total Billing by LOS Groups and Admission Type
                                              6. Treemap: Total Billing and Admitted Patients by Hospitals
                                              7. Pie Charts : Admitted Patients by Day Type, Admitted Patients by LOS Groups
                                              8. Matrix with Column Chart: Deieasewise Admitted Patients by Hospitals
                                                                           Patients Admission by Month and Day for the Selected Year
                                              9. Decomposition Tree: Total Billing by Hospitals, Admission Type, Age Groups, Gender
                                              
 ### iv. Insights and Recommendations

#### Summary Insights
                 
Total admitted patients count is strong with 11K–55K annually, showing steady growth.

Average age of patients is 51.8 years, indicating a majority mid-to-senior population.

Total billing exceeds $1.4B, suggesting high operational and revenue performance.

Average LOS ~15 days, meaning patient turnover is moderate but improvement is possible.

High abnormal test results (~54%) indicates significant chronic or critical illness volume.

35% inconclusive tests show need for better diagnostics or screening accuracy.

Houston Methodist Hospital has highest patient inflow and billing contribution.

Seasonal trends indicate lower admissions in early months (Feb–Mar) and summer dips (Jun–Jul).

Weekdays have more admissions than weekends, suggesting workday healthcare dependency.

Emergency & urgent cases show higher fluctuation compared to elective admissions.

Longest LOS (>15 days) generates highest revenue, especially for chronic treatment.

Senior age group (56–75) drives maximum billing, indicating major healthcare demand.

Female patients contribute higher revenue share than males.

Smaller hospitals provide lower billing share, showing uneven distribution of load.

Year-on-year figures reflect gradual improvement in billing, LOS efficiency & patient count.




#### Recommendations for Business Growth

Build senior-focused care programs (chronic disease packages, rehabilitation plans).

Improve lab testing & diagnostics quality to reduce inconclusive results.

Introduce optimized short-stay treatment pathways to reduce LOS and increase bed turnover.

Expand services and resources in high-revenue hospitals and uplift performance in lower-performing ones.

Promote elective surgery & preventive healthcare campaigns to boost stable revenue flow.

Use seasonal trend forecasting to manage staff, beds, and resource allocation efficiently.

 ## v. Data Source
 [Dataset in Microsoft Community](https://community.fabric.microsoft.com/t5/Data-Stories-Gallery/Healthcare-Analytics-Dashboard-Power-BI-Template/m-p/4788148)
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
![Healthcare Demographics Analysis](https://github.com/Morsshed/Power-BI-Healthcare-Analysis/blob/main/Healthcare%20Demographis%20Analysis.png?raw=true)
  ## C2 - Trend Analyses
![Healthcare Trend Analysis](https://github.com/Morsshed/Power-BI-Healthcare-Analysis/blob/main/Healthcare%20Trend%20Analysis.png?raw=true)
  ## C3 - Billing Analyses
![Healthcare Billing Analysis](https://github.com/Morsshed/Power-BI-Healthcare-Analysis/blob/main/Healthcare%20Billing%20Analysis.png?raw=true)

# D. Conclusion
I truly enjoyed working on this project from beginning to end. Experiencing the full process provided valuable insights into both the data and the visuals. I look forward to tackling similar projects in the future and exploring even more complex datasets.
