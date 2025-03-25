# Pizza_Place_Sales_PowerBI_Project

## Table of Contents
- [Project Download Link](#project-download-link)
- [Project Screenshots](#project-screenshots)
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning & Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Recommendations](#recommendations)
- [Limitations](#limitations)

---
### Project Download Link
- [Click Here to Download](https://github.com/alvincsh/Pizza_Place_Sales_PowerBI_Project/blob/main/Project%20and%20screenshots/Pizza%20Place%20Independent%20Project_AlvinCSH.pbix)
---

### <ins>Project Screenshots</ins>
![Pizza Place Independent Project Dashboard1_AlvinCSH](https://github.com/user-attachments/assets/d24c4ef2-d4f9-45d8-9981-57cd8a48660c)

![Pizza Place Independent Project Further Analysis page_AlvinCSH](https://github.com/user-attachments/assets/d1eb0d0b-fc50-49cc-8db0-06529b899f39)


---

### Project Overview

The aim of this project is to analyze the sales performance of a pizza place named **Plato's Pizza** over the past year to provide an overview of the sales performance, make recommendations to improve sales, and identify peak business hours.

### Data Sources

In this project, 4 separate CSV files obtained from the [Maven Analytics Website](https://mavenanalytics.io/data-playground) are utilized as listed below:

- order_details.csv
- orders.csv
- pizza_types.csv
- pizzas.csv
- [Click Here to Download the CSV files](https://github.com/alvincsh/Pizza_Place_Sales_PowerBI_Project/tree/main/pizza_sales%20source%20file%20from%20Maven%20Analytics)


### Tools

- PowerBI Desktop - Data Cleaning, Exploratory Data Analysis, Dashboard Report Visualization



### Data Cleaning and Preparation

The initial data preparation phase included the following steps:
1. Data Loading and Inspection
   - Includes enabling "Column Quality" and "Column Profile" under the "View" ribbon and "column profiling based on the entire data set"
2. Selecting the appropriate data type for each column
3. Data Cleansing and Formatting


### Exploratory Data Analysis

EDA involved exploring the datasets to answer several key questions, namely:

- What are the peak hours for the pizza place?
- What are the best selling and worst selling pizzas?
- How much sales was generated for the past year?
- Are there any pizzas that should be removed?
- Were there any unsold pizzas? If yes, which ones are they?
- What recommendations can be made to boost sales?

### Data Analysis

The changes performed to the specific data sheets in the "Transform Data" view is as follow:
- orders.csv
  1. Added Columns based on the *date* column:
     - Month Name
     - Quarter
     - Day of Week
     - Day Name
     - Day Name Abr. by using the "Extract - First Characters" to get the first 3 letters of the *Day Name* column
     - *Merged* Column which was renamed to "Quarter Name" by using the "Column From Examples" function
  2. Added Columns based on the *time* column:
     - Start of Hour
     - Hour

- pizza_types.csv
  1. Transform applied to "name" column:
     - The "Replace Values" function was used to remove the words "The" and "Pizza" from the data in the name column to provide a cleaner look to the visuals.

- pizzas.csv
 1. Added Conditional Column numbering sizes S,M,L,XL,XLL with 1,2,3,4,5 to allow the data in the size column to be ordered by this conditional column renamed as "size sorting column"
 2. In "Data View" after selecting the *size* column, under the "Column Tools" ribbon, select *"Sort by column" and choose *size sorting column* to ensure that the visualization will order the sizes S,M,L,XL,XXL accordingly.

- Unsold Items (new table)
  1. Created by first duplicating the order_details.csv table
  2. Merged Unsold Items table with the Pizzas table using a Full Outer Join and selected only the *pizza_id* column from it and had it renamed to "complete pizza_id".
  3. In "Data View" the DAX query used in the *New column* to identify the unsold pizzas by giving the number 1 to the null values in the *quantity* column by using the following DAX function:
    ``` unsold = IF('Unsold Items'[quantity] = BLANK(),1,BLANK()) ```

- order_details.csv
   1. In "Data View" a column was added using the DAX query:
      ``` price = RELATED(pizzas[price]) ```
   2. Another column to calculate the sales value of each order was named *sales* and was added afterwards using the following DAX query:
      ``` sales = order_details[quantity]*order_details[price] ```
#### Measures Table
  1. This table was created by clicking on "Enter data" in the Home ribbon, then renaming the table to *Measures Table* and by adding several New Measures before deleting the column inside the table.
  2. The measures created along with their DAX queries are as follows:
     - Total Sales ``` Total Sales = SUM(order_details[sales]) ```
     - Total Pizzas Sold ``` Total Pizzas Sold = SUM(order_details[quantity]) ```
     - Total Orders ``` Total Orders = DISTINCTCOUNT(order_details[order_id]) ```
     - Total Days ``` Total Days = DISTINCTCOUNT(orders[date]) ```
     - Avg Pizza Per Order ``` Avg Pizza Per Order = [Total Pizzas Sold]/[Total Orders] ```
     - Avg Pizzas Sold per Day ``` Average Pizzas Sold per Day = [Total Pizzas Sold]/ [Total Days] ```
     - Average Order Value ``` Average Order Value = [Total Sales]/[Total Orders] ```

### Results

The analysis results are as follows:
1. Total Sales generated in the past year was $817860
2. Total Orders made in the past year is 21,350
3. The Average Order Value (AOV) is $38 per order
4. On average, each order will have 2 pizzas
5. The total number of pizzas sold is 49,574
6. The peak period is between 1200HRS - 1359HRS on the weekdays
7. The best pizza by sales is *The Thai Chicken Pizza*
8. The worst pizza by sales is *The Brie Carre Pizza*
9. The average number of pizzas sold per day doesn't exceed 23 pizzas during the peak hours which indicates that the current number of seats available (15tables x4seats) is sufficient. (Assuming 1 pizza per person).


### Recommendations:

Based on the analysis, the following actions are recommended:
1. The operating hours should be reduced by 27%, from 0900hrs-2359hrs to 1100hrs-2159hrs to focus on the peak periods, as it only reduces sales by 3% but cuts more costs
2. The unsold pizzas namely Big Meat (Medium and Large), Five Cheese (Small and Medium), and Four Cheese (Small) should be removed from the menu to reduce losses due to wasted purchase of their ingredients.
3. The Greek pizza of XXL size, should be removed due to low market demand
4. Surveys should be done on the Big Meat pizza as its size S pizza had great demand but the M and L sized ones were unsold.
5. The Brie Carre Pizza offered only in S size, should be offered in larges sizes to test the market response as there was great demand.
6. The Chicken Alfredo Pizza sees great demand for its M size, but less for its L and S sizes. Bundle promotions could be offered to boost their sales.
7. The L sized Green Garden Pizza should be removed due to low sales.
8. The Thai Chicken Pizza should carry out some bundle promotions or discounts for the S and M sizes as they generate more than $5k in sales while the L size has generated close to $30k in sales.
9. The Greek Pizza of size XXL should be removed and more marketing focus should be on the S, M, and L sizes as the XL size has great sales.


### Limitations

1. Due to lack of data, assumptions on the number of customers per pizza ordered had to be made, which may affect the accuracy of the results obtained.
2. The data in this project is a fictitious and as such may not be applicable to real world scenarios.
3. Data on the sales of some of the pizzas may be incomplete, leading to less accurate recommendations.
4. Due to lack of space and to focus on the pizza analysis story, graphs for analyzing quarterly sales were not included in the final dashboard.

