# Power BI comparative analysis from scratch
## Project Overview
The purpose of this project is to conduct a comparative analysis of the sales and budgeted data of the Company for the fiscal year 2014-2020. The project aims to identify the variances between the actual and planned performance, Sales of current year vs previous year, analyze the causes and effects of the variances, and provide recommendations for improvement.

## Project Scope
The project scope includes the following activities:

Collected and organized the sales and budgeted data of the Company for the fiscal year 2014 to 2020.

Compared the actual and planned performance of the company using various metrics, such as Sales,Growth, Varience etc.

Identified and explained the positive and negative variances of budgets and Sales

Created insights for the comparative analysis of the sales and budget data

## Project Objectives: 
The project objectives are to:

* Provide a comprehensive and accurate report of the comparative analysis of the sales and budgeted data of Company for the years from 2014 to 2020.
* Highlight the Sales and Growth of the company’s performance 
* Support the strategic planning and decision-making of the company’s management and stakeholders

## Table of contents
* [Executive summary]()
  - [Project overview]()
  - [Project scope]()
  - [Project objective]()
* [Methodology]()
  - [Data collection]()
  - [Data Preparation and Analysis]()
  - [Modeling]()
  - [Visualization]()
* [Results and discussion]()

## Methodology
### Data collection: 
I obtained the sales and budget data of Company from 2014 to 2020 Provided on the Publically Available Datasets 

### Data Preparation and Analysis:
In power bi, I added the data from the excel file and it contains three tables (Sales, Budget, Product master), and loaded the data.

I used the ***calenderauto*** function by creating new table to select all the dates from the data.
          Date dim = CALENDARAUTO()

I separeted the months, dates, years From merged Date column by adding new colum using following ***DAX queries*** 

```
year = 'date dim'[Date].[Year]
For month month = 'date dim'[Date].[Month]
Qtr = 'date dim'[Date].[Quarter]
```

### Modeling:
Product manager is dimentional table and others are fact tables,these three tables are connected on the basis of product id.

I joined the table I created with dates on sales table and month on the budget table.

Hided the columns productid , months, date from product table and sales and budget so that we can only view the column we require in our comparative analysis.

### Visualization:

For Insights, some KPI's are required for that i used some queries 

```
cy sales =

VAR CY = MAX('date dim'[year])

return

CALCULATE(SUM(Sales[Sale Amount]),'date dim'[year]=CY)
```


```
py sales = CALCULATE([cy sales],SAMEPERIODLASTYEAR('date dim'[Date]))

```
```
YoY sales growth = DIVIDE([cy sales]-[py sales], [py sales], BLANK())
```


```budgeted sales = 

var cy = MAX('date dim'[year])

return

CALCULATE(SUM(Budget[Budgeted Amt]),'date dim'[year]= cy)
```
```
budgeted var% =  DIVIDE([cy sales]- [budgeted sales],[budgeted sales],BLANK())
```

* After these analysis I have added the some conditional formatting for the budgeted var and yoy sales growth as when it is positive it shows green and when negative its shown in red.

* Then I added slicer and add year months and qtr so we can see any specific data through that.

* I also added the tooltip so that I can the the information related to the selected items

### [TO VIEW THE DASHBOARD CLICK HERE](https://app.powerbi.com/view?r=eyJrIjoiMDA2ZjcxZGUtMTczNC00MzYzLWJmMTYtMGZkMjA5NWIzYjNjIiwidCI6IjgwMjQzZDFlLWI1ZGEtNGNjZS1iNTYwLWYwZDcxYzBjZjljZSJ9)




