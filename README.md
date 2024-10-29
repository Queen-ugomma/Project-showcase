Supplier Quality Insights Project
This project analyzes supplier quality data for a manufacturing company, focusing on defect quantity, downtime, and performance across various suppliers, materials, and plants.

Project Files
Raw Dataset (Excel file)
Power BI Dashboard pdf

Data Preparation
Initial Dataset: The original dataset, uploaded in Excel, contains unprocessed data from various plants.
Data Cleaning:
Performed in Power Query, where I removed duplicates and handled missing values.
Created additional tables to normalize the data into dimensions and facts:
Vendor Table
Plant Table
Material Table
Defect Type Table
Supplier Fact Table

DAX Calculations
Here is a structured view of the DAX calculations. Each calculation has a comment describing its purpose.

Impact Defect Type:

DAX
Impact Defect Type = 
VAR Impact = CALCULATE(COUNT('Supplier Fact'[Defect Type ID]), 
                       KEEPFILTERS('Defect Type'[Defect Type] = "Impact"))
VAR Defects = COUNT('Supplier Fact'[Defect Type ID])
RETURN DIVIDE(Impact, Defects)

No Impact Defect Type:

DAX
NoImpact Defect Type = 
VAR NoImpact = CALCULATE(COUNT('Supplier Fact'[Defect Type ID]), 
                         KEEPFILTERS('Defect Type'[Defect Type] = "No Impact"))
VAR Defects = COUNT('Supplier Fact'[Defect Type ID])
RETURN DIVIDE(NoImpact, Defects)

Rejected Defect Type:

DAX
Rejected Defect Type = 
VAR Rejected = CALCULATE(COUNT('Supplier Fact'[Defect Type ID]), 
                         KEEPFILTERS('Defect Type'[Defect Type] = "Rejected"))
                         
VAR Defects = COUNT('Supplier Fact'[Defect Type ID])
RETURN DIVIDE(Rejected, Defects)
Total Defect Quantity:

DAX
Total Defect QTY = SUM('Supplier Fact'[Total Defect Qty])
Month-over-Month Defect Quantity:

DAX
Total Defect QTY PM = CALCULATE([Total Defect QTY], 
                                PARALLELPERIOD('Date'[Date], -1, MONTH))
                                
Defect Quantity Trend Icon (Month-over-Month):

DAX
MOMDefect QTY Trend Icon = 
VAR positiveicon = UNICHAR(9650)
VAR negativeicon = UNICHAR(9660)
VAR choice = IF([MOMGrowthDefectQTY] > 0, positiveicon, negativeicon)
RETURN choice & " " & FORMAT([MOMGrowthDefectQTY], "0.00%")

Total Downtime Hours:

DAX
Total Downtime HRS = [Total Downtime Minutes] / 60

Month-over-Month Downtime Trend Icon:

DAX
MOMDowntime HRS Trend Icon = 
VAR positiveicon = UNICHAR(9650)
VAR negativeicon = UNICHAR(9660)
VAR choice = IF([MOMGrowthDowntimeHRS] > 0, positiveicon, negativeicon)
RETURN choice & " " & FORMAT([MOMGrowthDowntimeHRS], "0.00%")
(Add additional DAX calculations as needed based on the full list provided earlier.)

Visualizations
In Power BI, I created several visualizations to show insights, including:

Top and Bottom Performing Vendors and Plant Performance: Bar chart
Vendor Risk Levels: Scatter plot showing high, medium, and low-risk vendors
