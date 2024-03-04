Project 2


# Grocery (Maven Market) Store Analysis

### Dashboard Link : https://app.powerbi.com/groups/me/reports/ff90be76-5046-4487-ae74-bff797e4c365/ReportSection5e991c1086309a89a687?experience=power-bi

## Problem Statement

The Maven Market represents a grocery store that sells food and household supplies to North and Central American markets. The dataset contains 
* **Product data** (Product ID, Product Brand, Retail Price, etc.,)
* **Customer data** (Customer ID, Firstname, Customer Address, birthdate, etc.,)
* **Region data** (Region ID, Sales District, Sales Region)
* **Store data** (Store ID, Store Type, Store City, Store Opened Date, etc.,)

The following dashboards helps paint a picture as to how various store operates under changing circumstances.

* **Topline Performance** - Provides an overview into the (grocery) store-related KPIs for North and Central American regions


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present
- Step 5 : In the report view, under the view tab, theme was selected
- Step 6 : In the report view, under the insert tab, using shapes option from elements group a rectangle was inserted & similarly using image option company's logo was added to the report design area
- Step 7 : Multiple **Calculated Columns** were created in which, 
  - Customers were segmented into priority levels
  - Products were segments into tier lists and so on


For creating new Calculated Columns following DAX expression was written;

Year Since Remodel (In Product data Veiw)
        
       Year_Since_Remodel = 
                          YEAR(TODAY()) - YEAR(Stores[last_remodel_date])

![snip2_cal_col_2](https://github.com/avinashSQL/Data-Analytics-Portfolio/assets/82948527/b59da105-2158-47e8-a7ea-88e0152797ae)


Customer Priority (In Customer data Veiw)
        Priority = 
                SWITCH(
                    TRUE(),
                    Customers[homeowner] = "Y" && Customers[member_card] = "Golden", "High",
                    "Standard")

![snip2_cal_col_1](https://github.com/avinashSQL/Data-Analytics-Portfolio/assets/82948527/3ddc2992-bcdb-4a86-b93e-286e0796d04a)

        
- Step 8 : New measure was created to find total profit, total transactions to name a few (total 21 Measures were calculated for this project)

Following DAX expression for **Total Revenue** is as follows,
        
        Total Revenue = 
                      SUMX(
                          Transaction_Data,
                          Transaction_Data[quantity] * Transaction_Data[retail_price])       
A card visual was used to represent Total Revenue (in $)

![snip2_measure_1](https://github.com/avinashSQL/Data-Analytics-Portfolio/assets/82948527/afc30596-89d3-43a3-b892-b0e46ced6fb6)

Following DAX expression for **Total Cost** is as follows,

          Total Cost = 
                    SUMX(
                        Transaction_Data,
                        Transaction_Data[quantity] * Transaction_Data[product_cost_trans])

A card visual was used to represent Total Cost (in $)

![snip2_measure_3](https://github.com/avinashSQL/Data-Analytics-Portfolio/assets/82948527/76fca469-9e16-4e6c-8c91-75e3ef05d194)

Following DAX expression for **Total Profit** is as follows,

          Total Profit = 
                      [Total Revenue] - [Total Cost]

A card visual was used to represent Total Profit (in $)

![snip2_measure_4](https://github.com/avinashSQL/Data-Analytics-Portfolio/assets/82948527/1e04f913-e88a-4963-bdb4-9f996ce0bf04)


        
 - Step 9 : New measure was created to find **Last Month Revenue** (in $)
 
 Following DAX expression was written to find % of customers,
 
       Last Month Revenue = 
                          CALCULATE(
                              [Total Revenue],
                              DATEADD(
                                  'Calendar'[date],
                                  -1,
                                  MONTH))
 
 A card visual was used to represent Last Month Revenue (in $)
 

![snip2_measure_5](https://github.com/avinashSQL/Data-Analytics-Portfolio/assets/82948527/dac1fd74-8a30-40e4-947d-b96ea22162fb)

 
 - Step 10 : New measure **Return Rate** was created to calculate %  of items returned and a card visual was used to represent the same
 
 Following DAX expression was written to find total distance,
 
         Return Rate = 
                    DIVIDE(
                        [Quantity Returned],
                        [Quantity Sold],
                        "No Sales")
    
 A card visual was used to represent this total distance. 
 
![snip2_measure_6](https://github.com/avinashSQL/Data-Analytics-Portfolio/assets/82948527/f80409d3-1247-480a-9e33-e8f556368407)
 
 - Step 11 : The report was then published to Power BI Service.
 
 
![snip2_publish](https://github.com/avinashSQL/Data-Analytics-Portfolio/assets/82948527/9d5dadf0-61ea-4031-baaa-2dae0e6b7900)

# Snapshot of Exec Dashboard

![snip2_pic1](https://github.com/avinashSQL/Data-Analytics-Portfolio/assets/82948527/fddeeb24-8f7e-42f7-a6e2-a453a1d796e3)

 # Insights

A multiple page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the Topline Dashboard for the year 1998,

### [1] Top 3 Products Sold Globally  

  - #### Hermanos

    Number of Transactions = 5,342

    Total Profit = $21,753

     Profit Margin = 58.64%

  - #### Ebony

    Number of Transactions = 5,238

    Total Profit = $20,354

    Profit Margin = 59.81%

  - #### Tell Tale

    Number of Orders = 5,112

    Revenue = $19,982

    Return Rate = 58.05%

      
           Hermano is the favorite grocery item across all 3 countries i.e., USA, Canada, and Mexico

### [2] Year-to-Date Revenue 

  YTD Revenue (1997) = $565.238

  YTD Revenue (1998) = $1,199,308

           YTD Revenue is increases over time, indicating upward trajectory of buisness topline
           
### [2] Product-level Inferences

    a) Most Purchased Item on Weekend - CLub Whole Milk (40.67%)
    b) Heighest Porfit Margin - Landslide Sesame Oil (70.69%)
    c) Heightest Returned Product - Shady Lake Spaghetti (2.93%)
    d) Lowest Product Sold (in Quantities) - CDR Apple Preserves (240 units)

 ### [3] Location-based Inferences

  ### Total Customers
 
The heighest number of customers are from the Unied States of America, i.e, **7,359** customers. Followed by Canada, i.e., **1717** Customers. Mexico ranks last for customer count, i.e, **1205** customers
 
 ### Total Profit (Turnover)
 
**USA** customers contribute heighest profit earned by the company at **$ 702,790**

**Canada** records the least profit earned metrics at **$ 64,341**
 
          Thus, USA and Mexico markets present greater potential for expanding store locations.
 
 ### Demography Metrics 
 
 -  71.21 % married customers are from the USA
 
 -  Only 11.78 % Mexican customers have children (lowest) 
 
 -  72.1 % American customers are male

 -  Only 12.1 % Mexican customers are female
 
         Thus, maximum customers belong to '50-55' age group
         
### Customer Type

- 89.9 % customers are 'Parents'

- 60.1 % customers are 'Home Owners'
       
       thus, most customers are 'Parents & Home Owners'
