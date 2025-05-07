📌 Project Overview
This Power BI report was built using data related to Plant Production and Sales.
The purpose of the report is to analyze Gross Profit, Sales, and Quantity dynamically over different periods, allowing easy comparison between timeframes.

** The report includes:
- Clean and optimized data modeling.
- Dynamic calculations via DAX Measures.
- User-friendly slicers and interactive button filters.
- Clear and minimalistic visual design.


📊 Data Model
** Summery Of The Data 
1. Plant_FACT : Contains sales transaction data, Each row represents a sale of a product.
- Product_id: Unique product ID.
- Sales_USD: Sales value in US dollars.
- Quantity: Number of units sold.
- Price_USD: Price per unit.
- COGS_USD: Cost of Goods Sold.
- Date_Time: Transaction date.
- Account_id: Links to the customer account.

2. Accounts : Contains customer/account information.
- country_code, country2: Customer's country.
- Account: Customer or company name.
- latitude2, longitude: Customer location coordinates.
- Postal_code, street_name, Street_number: Customer address.
- Account_id: Links customers to sales records.

3. Plant_Hierarchy : Contains product/plant classification details.
- Product_Family: Main plant family.
- Product_Group: Subgroup within the family.
- Product_Name: Scientific name of the product.
- Product_Size: Size of the product (Small, Medium, Large).
- Produt_Type: Usage type (e.g., Landscape, Outdoor).

4. Dim_Date : Created manually using DAX:
- Dim_Date = CALENDAR(DATE(2022,01,01), DATE(2024,12,31))
- InPast Column :Added to the Dim_Date table to filter dates correctly.


🛠 Measures
- Sales = SUM(Fact_Table[Sales])
Calculates total sales amount.
- Gross Profit = [Sales] - [COGs]
Calculates Gross Profit value (Sales - Costs).
- Quantity = SUM(Fact_Table[Quantity])
Calculates total quantity sold.
- GP% = DIVIDE([Gross Profit],[Sales])
Compares Gross Profit This Year vs Last Year sales

- YTD_Sales = TOTALYTD([Sales], Fact_Sales[Date_Time])
Sales from the beginning of This Year.
- YTD_Quantity = TOTALYTD([Quantity], Fact_Sales[Date_Time])
Quantity from the beginning of This Year.
- YTD_GrossProfit = TOTALYTD([Gross Profit], Fact_Sales[Date_Time])
Gross Profit from the beginning of This Year.

- PYTD_Sales = CALCULATE([Sales], SAMEPERIODLASTYEAR(Dim_Date[Date]))
Calculates sales for Last Year
- PYTD_Quantity = CALCULATE([Quantity],SAMEPERIODLASTYEAR(Dim_Date[Date]),Dim_Date[InPast] = TRUE)
Calculates Quantity for Last Year
- PYTD_GrossProfit = CALCULATE([Gross Profit],SAMEPERIODLASTYEAR(Dim_Date[Date]),Dim_Date[InPast] = TRUE)
Calculates Gross Profit for Last Year

- YTD vs PYTD : Compares This year to Previous Year
- S_PYTD, S_YTD : Switches For Slicer


🎯 Visuals Used
- Card		: Displays KPIs like Sales, Quantity, and Gross Profit for ( YTD, YTD vs PYTD, PYTD and GP% ).
- Line Chart	: Shows Sales, Quantity and Gross Profit trend over time.
- Donut Chart	: Shows Sales, Quantity and Gross Profit by Product Type.
- Bar Chart	: Comparison between current and previous year by Country.

🧩 Filters and Slicers
- Button Slicers : Allow users to select between Sales, Quantity, or Gross Profit dynamically.
- Date Slicer	 : Limits data to years.

💡 Report Features :
- Organized Measures into Folders for easy maintainability.
- Dynamic switching of KPIs makes the report flexible without duplicating visuals.
- Using InPast logic ensures the report remains clean and logical over time.
- KPI Cards display detailed values for easy understanding without opening charts.


