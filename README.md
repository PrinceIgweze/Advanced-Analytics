# E-Commerce Inventory Analysis

## Task

A successful data analysis project starts by identifying the questions our user group needs answered. Sometimes, users might not know exactly what they need until they see some visualizations. As a data analyst, I created a few visuals using the available data and brainstormed with the users to frame specific business questions. For this analysis, our user group is interested in understanding:

- How their inventory is performing
- Stock on hand performance
- If low stock is costing them a fortune

## My Approach

I applied a conventional data analysis methodology. Based on the questions raised by our user group, I identified the domain as **inventory** and **stock performance analysis**. Key points of interest for analysis include:

- Stock on hand amounts
- Stock orders (Backorders)
- Stock costs
- Impact of stock levels
- Overstock cost
- Lost sales due to lack of stock

These measures provide analytical insight into how the user’s stock and inventory are performing.

![Flow Chart](https://github.com/PrinceIgweze/Inventory-Data-Analysis/blob/main/Flow%20Diagram.png)
*Figure 1: Process Flow Chart*
### Task Approach

For my dashboards, I determined that two dashboards would be optimal:

1. **Dashboard #1: Stock Performance**
   - Designed for desktop interaction
   - Questions to be answered:
     - Stock on hand total
     - Stock on hand cost as a trend over time
     - Stock Status Count
     - Order Total (Backorders)
     - Lost sales due to back order trend over time
     - Back order status
     - Slicing by year, month, product, and subcategory

2. **Dashboard #2: Overstock Performance**
   - Designed for mobile devices (e.g., iPad)
   - Questions to be answered:
     - Overstock total
     - Overstock total cost
     - Overstock on hand total as a trend line
     - Slice by year, month, product, and subcategory
       
![Flow Chart](https://github.com/PrinceIgweze/Inventory-Data-Analysis/blob/main/Metrics%20Table.png?raw=true)
*Figure 2: Metrics Table*    


## Table of Metrics and Data Source Tables

### Business Rules

I applied the following business rules for calculating metrics using SQL on Microsoft SQL Server. This approach helps prevent importing unnecessary data columns and reduces dependency on specific visualization tools.

- **Stock on Hand Value:** Sum of all stock quantities recorded in the system.
- **Backorder Count:** Count of all backorders recorded in the system.
- **Stock Status Calculation:**
  - `Stock on hand >= Stock reorder point`: Stock level is okay.
  - `Stock on hand = 0 and Backorders > 0`: Out of stock but in order.
  - `Stock on hand < Reorder point and Backorders > 0`: Stock is low but in order.
  - `Backorders = 0 and Stock on hand <= Reorder point`: Time to order.
- **Backorder Status Calculation:**
  - `Backorders > 0 and <= 10`: Status will be up to 10 on order.
  - `Backorders > 10 and < 20`: Status will be up to 20 on order.
  - `Backorders > 20 and <= 40`: Status will be up to 40 on order.
  - `Backorders > 40 and < 60`: Status will be up to 60 on order.
- **Stock on Hand Cost:** `Stock on hand * Product unit cost`
- **Lost Sale Value:** `Number of backorders * Product list price`
- **Overstock on Hand Value:** `Stock quantity - Product maximum stock level allowed`

[Click to View SQL Query Code](https://github.com/PrinceIgweze/E-Commerce-Inventory-Performance-Analysis/blob/main/Inventory%20Analysis%20SQL%20Query.sql)

## Analysis

![Flow Chart](https://github.com/PrinceIgweze/E-Commerce-Inventory-Performance-Analysis/blob/main/Ecommerce%20Stock%20Performance%20-%20Tableau.png?raw=true)
*Figure 3: Ecommerce Stock Performance*    

### Stock Performance

Analyzing the stock on hand cost, I found that it increases throughout the year and dips towards the end of the year, particularly in December and January. This suggests that inventory management may be ineffective. Lost sales analysis in 2018 showed a significant loss for projectors and screens, despite having reasonable stock on hand. This points to inefficiencies in placing backorders when reasonable stock is available.

![Flow Chart](https://github.com/PrinceIgweze/E-Commerce-Inventory-Performance-Analysis/blob/main/General%20Ecommerce%20Performance.png?raw=true)
*Figure 4: General Ecommerce Performance*  

### Overstock Performance

The overstock performance dashboard confirms that overstock amounts peak at the end of the year, causing additional costs. The car video and laptop product categories have the highest overstock costs.

## Recommendations

Based on the analysis:

- Implement more efficient management of stock on hand and backorders, especially during January and December, to reduce costs.
- Focus on the car, video, and laptop product categories to address overstock issues.
