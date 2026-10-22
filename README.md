# Northwind Sales & Business Performance Analysis

**Author:** Yekini Abdulroqeeb Ademola  
**Programme:** Techie Academy Capstone Project  
**Project type:** Business intelligence and sales performance analysis  
**Tools:** Microsoft Power BI Desktop, SQLite, SQLite3 ODBC Driver, Power Query, DAX, GitHub

## Table of contents

- [Project overview](#project-overview)
- [Business problem](#business-problem)
- [Project objectives](#project-objectives)
- [Dataset description](#dataset-description)
- [Database structure](#database-structure)
- [Tools and technologies](#tools-and-technologies)
- [Data preparation and data model](#data-preparation-and-data-model)
- [Analysis performed](#analysis-performed)
- [Dashboard preview](#dashboard-preview)
- [Key insights](#key-insights)
- [Recommendations](#recommendations)
- [Project structure](#project-structure)
- [How to access and use the project](#how-to-access-and-use-the-project)
- [Limitations and interpretation notes](#limitations-and-interpretation-notes)
- [Author](#author)

## Project overview

This capstone project uses the Northwind sample business database to examine historical sales and related operations. The analysis was developed in Microsoft Power BI to turn order-level data into interactive reports that help management explore revenue, product performance, customers, employee-associated sales, and shipping activity.

The Power BI report contains six pages:

1. Executive Overview
2. Sales Analysis
3. Product Performance
4. Customer Analysis
5. Employee/Sales Performance
6. Shipping & Operations

The repository includes the SQLite database, the Power BI report, dashboard screenshots, a CEO presentation, presenter notes, and supporting project documentation.

## Business problem

Management needs a clear view of sales and operational performance but transactional records alone do not make it easy to identify the most important products, customers, markets, employee-associated sales results, or shipping issues. This project organizes the available Northwind data into an interactive report so users can compare performance across products, categories, customers, countries, employees, dates, and shipping providers.

The analysis is intended to support evidence-based decisions. It does not, by itself, establish product profitability, explain the causes of sales changes, or measure actual delivery arrival times.

## Project objectives

- Summarize overall business performance using key performance indicators (KPIs).
- Examine sales revenue and order activity over time.
- Identify high-revenue and high-volume products, best-performing categories, and products with low sales or high recorded inventory.
- Compare customer revenue, order frequency, and geographic sales contribution.
- Review employee-associated sales using revenue, order count, average order value, and revenue contribution.
- Examine order volume by shipper, freight costs, shipping patterns, and recorded shipment timeliness.
- Present key findings and practical recommendations in a multi-page Power BI report and CEO presentation.

## Dataset description

The source file is [`Northwind.db`](./Northwind.db), a SQLite database containing historical order, product, customer, employee, supplier, and shipping-related records.

### Dataset snapshot

| Item | Recorded value |
|---|---:|
| Orders | 830 |
| Customers | 93 |
| Products | 77 |
| Employees | 9 |
| Suppliers | 29 |
| Product categories | 8 |
| Order details / line items | 2,155 |
| Recorded order-date range | 4 July 1996 – 6 May 1998 |
| Revenue shown in the report | Approximately $1.35 million |

Revenue is presented as approximately $1.35 million because the dashboard displays rounded figures. The order-date range and row counts above were checked against the supplied database.

## Database structure

The SQLite source contains 11 tables. The table counts below are based on the uploaded `Northwind.db` file.

| Table | Rows | Purpose |
|---|---:|---|
| `Categories` | 8 | Product category names and descriptions |
| `Customers` | 93 | Customer companies and contact/location details |
| `EmployeeTerritories` | 49 | Links employees to sales territories |
| `Employees` | 9 | Employee details |
| `OrderDetails` | 2,155 | Product line items, unit prices, quantities, and discounts for orders |
| `Orders` | 830 | Order dates, customer and employee references, shipping details, and freight |
| `Products` | 77 | Product names, category/supplier references, prices, and stock fields |
| `Region` | 4 | Region descriptions for the territory structure |
| `Shippers` | 3 | Shipping company details |
| `Suppliers` | 29 | Supplier company and contact details |
| `Territories` | 53 | Sales territory descriptions and region references |

### Main logical relationships

The database keys support the following relationships, which should be checked in Power BI Model view if the model is changed:

- `Customers.CustomerID` → `Orders.CustomerID`
- `Employees.EmployeeID` → `Orders.EmployeeID`
- `Orders.OrderID` → `OrderDetails.OrderID`
- `Products.ProductID` → `OrderDetails.ProductID`
- `Categories.CategoryID` → `Products.CategoryID`
- `Suppliers.SupplierID` → `Products.SupplierID`
- `Shippers.ShipperID` → `Orders.ShipVia`
- `Employees.EmployeeID` → `EmployeeTerritories.EmployeeID`
- `Territories.TerritoryID` → `EmployeeTerritories.TerritoryID`
- `Region.RegionID` → `Territories.RegionID`

`Orders` and `OrderDetails` provide the main transactional data for order and sales analysis. The other tables provide descriptive details used to group and interpret those transactions. The Power BI report also includes a date table with Year, Quarter, Month Name, Month Number, and Year-Month fields for time-based reporting.

## Tools and technologies

- **Microsoft Power BI Desktop:** Builds the interactive, six-page report and KPI cards.
- **SQLite:** Stores the source dataset in `Northwind.db`.
- **SQLite3 ODBC Driver (64-bit):** Connection method documented for loading the SQLite database into Power BI Desktop.
- **Power Query:** Used within the Power BI workflow for data import and preparation where required.
- **DAX:** Defines report measures and calculations for metrics such as revenue, orders, customers, products, quantity sold, average order value, and contribution analysis.
- **GitHub:** Hosts the project files, README, screenshots, and supporting deliverables.

## Data preparation and data model

The documented source connection uses the 64-bit SQLite3 ODBC Driver and a System Data Source Name (DSN) called `Northwind_SQLite`.

The documented connection workflow is:

1. Install the 64-bit SQLite3 ODBC Driver.
2. Configure the `Northwind_SQLite` DSN to point to `Northwind.db` using Windows ODBC Data Source Administrator.
3. In Power BI Desktop, choose **Get Data → ODBC** and select the configured DSN.
4. Load the required source tables and review their data types and relationships.
5. Use the date table fields for year, quarter, month, and year-month comparisons.
6. Use report measures to summarize sales and operational activity in the visuals.

The model links orders and order-detail records to descriptive tables such as customers, employees, products, categories, and shippers. Review the relationship directions and date relationship in Model view before adapting the report or refreshing it with a different data source.

For the detailed connection notes, see [`NORTHWIND CAPSTONE PROJECT DOCUMENTATION.docx`](./documentation/NORTHWIND%20CAPSTONE%20PROJECT%20DOCUMENTATION.docx).

## Analysis performed

### Executive overview

- Total revenue, total orders, customers, products, and quantity sold.
- Sales trend over time.
- Sales by country and category.
- Top products by revenue.
- Key business highlights.

### Sales analysis

- Sales by year and month.
- Sales trend over time.
- Revenue by country and product category.
- Top products and top customers by revenue.

### Product performance

- Top products by quantity sold.
- Top products by revenue.
- Best-performing product categories.
- Bottom products by quantity sold.
- Products with high recorded inventory.
- Count of discontinued products.

### Customer analysis

- Number of customers.
- Sales by country.
- Top customers by revenue and order count.
- Customer contribution to revenue.

### Employee/sales performance

- Sales by employee.
- Number of orders handled by each employee.
- Revenue contribution by employee.
- Average order value by employee.
- Employee-associated sales over time.

### Shipping and operations

- Orders handled by each shipper.
- Freight costs by shipper.
- Shipping activity over time.
- Recorded on-time, late, and not-shipped status based on available order dates.
- Shipping activity by country.

## Dashboard preview

The screenshots below are stored in the repository's `screenshots/` folder.

### Executive Overview

![Executive Overview dashboard](screenshots/executive-dashboard.png)

### Sales Analysis

![Sales Analysis dashboard](screenshots/sales-analysis.png)

### Product Performance

![Product Performance dashboard](screenshots/product-performance.png)

### Customer Analysis

![Customer Analysis dashboard](screenshots/customer-analysis.png)

### Employee/Sales Performance

![Employee/Sales Performance dashboard](screenshots/employee-sales-performance.png)

### Shipping & Operations

![Shipping & Operations dashboard](screenshots/shipping-operations.png)

## Key insights

1. **Overall sales:** Northwind generated approximately $1.35 million across 830 orders during the recorded period. 1997 had the highest annual revenue in the report, at approximately $660,000. Since 1996 and 1998 are partial years, annual totals are not like-for-like comparisons.
2. **Product and category mix:** Côte de Blaye generated approximately $150,000 in revenue, while Camembert Pierrot led by quantity sold. Beverages generated the highest category revenue, followed by Dairy Products. Eight products are marked as discontinued.
3. **Customers and markets:** The USA led sales revenue, followed by Germany and Austria. QUICK-Stop generated approximately $117,480, slightly ahead of Save-a-lot Markets at approximately $115,670; Save-a-lot Markets recorded more orders.
4. **Employee-associated sales:** Margaret was associated with approximately $250,190 in revenue (18.47% in the displayed employee contribution breakdown) and handled around 156 orders. Robert had the highest average order value in the report, at approximately $1,950. These measures alone do not establish individual productivity.
5. **Shipping records:** 772 orders were shipped on or before their recorded required dates, 37 were shipped late, and 21 had no recorded shipped date. United Package handled the most orders and had the highest total freight in the report. Total freight should be interpreted alongside shipment volume.

## Recommendations

- Compare equivalent monthly or year-to-date periods when monitoring revenue, order count, and average order value.
- Monitor high-revenue and high-volume products separately, compare stock levels with sales activity, and review replacement options for discontinued products.
- Maintain relationships with high-value customers and monitor changes in their order frequency, revenue, and average order value.
- Evaluate employee-associated sales using multiple measures and consider differences in workload, customer assignments, and time period before drawing conclusions about productivity.
- Investigate the 37 late shipment records and the 21 orders without a recorded shipped date.
- Compare shipping providers using average freight cost per order and recorded shipment timeliness, not total freight alone.

## Project structure

```text
Northwind-business-analysis/
├── README.md
├── .gitignore
├── Northwind.db
├── powerbi/
│   └── Northwind_Analysis.pbix
├── presentation/
│   ├── Northwind_CEO_Presentation.pptx
│   ├── Northwind_CEO_Presentation.pdf
│   └── Northwind_CEO_Presenter_Notes.docx
├── pdf/
│   └── Northwind_Business_Insights_and_Recommendations.pdf
├── screenshots/
│   ├── executive-dashboard.png
│   ├── sales-analysis.png
│   ├── product-performance.png
│   ├── customer-analysis.png
│   ├── employee-sales-performance.png
│   └── shipping-operations.png
└── documentation/
    ├── NORTHWIND CAPSTONE PROJECT DOCUMENTATION.docx
    ├── Northwind_Business_Insights_and_Recommendations.docx
    └── Techie_Academy_Capstone_Project_Brief.pdf
```

## How to access and use the project

1. Download or clone this repository from GitHub.
2. Open `Northwind_Analysis.pbix` in Microsoft Power BI Desktop.
3. The SQLite source file is included as `Northwind.db` in the repository root. If Power BI requests a data source, configure the SQLite3 ODBC Driver and point the `Northwind_SQLite` DSN to your local copy of that database.
4. Refresh the data if required, and confirm that the measures and visuals update as expected.
5. Use the six report page tabs to explore the analysis.
6. Review the CEO presentation in `presentation/` and the supporting findings and recommendations in `pdf/` and `documentation/`.

The screenshots and report are provided as supporting project deliverables. The `.pbix` file is the interactive report; screenshots are static previews.

## Limitations and interpretation notes

- The data covers 4 July 1996 through 6 May 1998, and 1996 and 1998 are incomplete calendar years.
- Revenue is not the same as profit. The report does not establish product profit margins because complete product cost and profitability information is not presented in these visuals.
- The shipment-status analysis compares recorded `ShippedDate` with `RequiredDate`; it does not measure the actual date an order arrived with a customer.
- Orders with no recorded shipped date may reflect missing information or orders not yet shipped; the available data alone does not establish the reason.
- Higher revenue, more orders, or higher average order value should not be treated as proof of employee productivity without considering workload, customer assignments, and other context.
- Dashboard values marked approximately are rounded readings from the report and should be checked against the refreshed Power BI file before formal reuse.

## Author

**Yekini Abdulroqeeb Ademola**  
Techie Academy Capstone Project  
**Project:** Northwind Sales & Business Performance Analysis
