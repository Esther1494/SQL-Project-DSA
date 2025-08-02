# 📊 KMS Sales Intelligence with SQL Server (2009–2012)

Welcome to my SQL case study project! This analysis was conducted as part of my training at **Digital SkillUp Africa (DSA)**. It focuses on historical order data from **Kultra Mega Stores (KMS)**, a Nigerian retail and wholesale company operating across several regions between **2009 and 2012**.

In this project, I used **SQL Server Management Studio (SSMS)** to clean, query, and analyze transactional data, answering key business questions and offering actionable recommendations.

---

## 1. 🚀 Project Objectives

KMS management requested actionable insights into:

- Product category and regional performance
- Customer behavior across business segments
- Shipping cost and delivery efficiency
- Recommendations to increase profitability

**My responsibilities included:**

- Importing CSV data into SQL Server
- Data type optimization and cleaning
- Writing SQL queries to solve real business problems
- Delivering insight-based recommendations

---

## 2. 🛠 Tools & Technologies Used

| Tool                                | Purpose                                       |
|-------------------------------------|-----------------------------------------------|
| SQL Server Management Studio (SSMS) | Querying and analysis                         |
| Flat File Import Wizard             | CSV data import                               |
| T-SQL                               | Writing queries and data transformations      |
| Microsoft Excel                     | Preliminary inspection and validation         |
| GitHub                              | Version control and project documentation     |

---

## 3. 📥 Data Import Process

- **File Type**: CSV (Flat file)
- **Import Tool**: SSMS Flat File Import Wizard
- **Table Name**: `KMS`

### 🔄 Data Type Adjustments:
| Column            | Updated Data Type     |
|-------------------|------------------------|
| `Sales`           | `DECIMAL(10,2)`        |
| `Profit`          | `DECIMAL(10,2)`        |
| `Discount`        | `DECIMAL(10,2)`        |
| `Shipping_Cost`   | `DECIMAL(10,2)`        |
| `Quantity`        | `INT`                  |
| `Order_ID`        | `INT`                  |

---

## 4. 🔍 Business Questions & SQL Queries

### 4.1. Which product category had the highest number of orders?
```sql
SELECT TOP 1 Product_Category, COUNT(*) AS Product_Count
FROM KMS
GROUP BY Product_Category
ORDER BY Product_Count DESC;
```

### 4.2. What are the top 3 and bottom 3 regions in terms of sales?
```sql
-- Top 3 regions
SELECT TOP 3 Region, SUM(Sales) AS Total_Sales
FROM KMS
GROUP BY Region
ORDER BY Total_Sales DESC;

-- Bottom 3 regions
SELECT TOP 3 Region, SUM(Sales) AS Total_Sales
FROM KMS
GROUP BY Region
ORDER BY Total_Sales ASC;
```

### 4.3. What were the total sales in Ontario?
```sql
SELECT Region, SUM(Sales) AS Total_Sales
FROM KMS
WHERE Region = 'Ontario'
GROUP BY Region;
```

### 4.4. How can KMS improve revenue from the bottom 10 customers?
```sql
SELECT TOP 10 Customer_Name, SUM(Sales) AS Total_Sales
FROM KMS
GROUP BY Customer_Name
ORDER BY Total_Sales ASC;
```
💡 **Recommendations:**
- Create personalized marketing and promo offers
- Launch loyalty reward programs
- Follow up with low-engagement customers via email
- Offer discounts or bundles to encourage repeat purchases

### 4.5. Which shipping method incurred the most cost?
```sql
SELECT TOP 1 Ship_Mode, SUM(Shipping_Cost) AS Total_Shipping_Cost
FROM KMS
GROUP BY Ship_Mode
ORDER BY Total_Shipping_Cost DESC;
```

### 4.6. Who are the most valuable customers and what products do they buy?
```sql
SELECT Customer_Name, Product_Name, SUM(Sales) AS Total_Sales
FROM KMS
GROUP BY Customer_Name, Product_Name
ORDER BY Total_Sales DESC;
```

### 4.7. Which small business customer had the highest sales?
```sql
SELECT TOP 1 Customer_Name, SUM(Sales) AS Total_Sales
FROM KMS
WHERE Customer_Segment = 'Small Business'
GROUP BY Customer_Name
ORDER BY Total_Sales DESC;
```

### 4.8. Which corporate customer placed the most orders?
```sql
SELECT TOP 1 Customer_Name, COUNT(Order_ID) AS Total_Orders
FROM KMS
WHERE Customer_Segment = 'Corporate'
GROUP BY Customer_Name
ORDER BY Total_Orders DESC;
```

### 4.9. Which consumer customer was the most profitable?
```sql
SELECT TOP 1 Customer_Name, SUM(Profit) AS Total_Profit
FROM KMS
WHERE Customer_Segment = 'Consumer'
GROUP BY Customer_Name
ORDER BY Total_Profit DESC;
```

### 4.10. Which customers returned items and what segments do they belong to?
```sql
SELECT DISTINCT K.Customer_Name, K.Customer_Segment, O.Status
FROM KMS K
JOIN Order_Status O ON K.Order_ID = O.Order_ID
WHERE O.Status = 'Returned';
```

### 4.11. Was shipping method aligned with order priority?
```sql
SELECT Order_Priority, Ship_Mode,
       COUNT(Order_ID) AS Order_Count,
       SUM(Shipping_Cost) AS Total_Shipping_Cost,
       AVG(DATEDIFF(DAY, Order_Date, Ship_Date)) AS Avg_Shipping_Days
FROM KMS
GROUP BY Order_Priority, Ship_Mode
ORDER BY Order_Priority, Ship_Mode;
```
🧠 **Insight:**  
Fast shipping (Express Air) was underutilized for urgent orders, while cheaper but slower methods were overused. This mismatch increased delivery delays and unnecessary costs.

---

## 5. 📊 Key Findings Summary

| Metric                      | Finding                          |
|-----------------------------|----------------------------------|
| 🛒 Most Sold Category        | Office Supplies                  |
| 🌍 Best Sales Region         | West                             |
| ❌ Weakest Sales Region      | Nunavut                          |
| 💰 Most Profitable Segment   | Consumer                         |
| 🚚 Costliest Shipping Method | Express Air                      |
| ⚠️ Operational Risk          | Misaligned shipping priorities   |

---

## 6. 📈 Business Recommendations

- 🚚 Use Express Air only for **high-priority orders**
- 🎯 Target top-performing regions with **seasonal campaigns**
- 🔁 Re-engage bottom-tier customers with **discounts & bundles**
- 📦 Reduce overuse of heavy shipping for low-value orders
- 🧮 Optimize product pricing using **sales and profit trends**

---

## 7. 📁 Repository Structure

```
kms-sql-analysis/
├── README.md                      # This documentation
├── data/
│   └── kms_orders.csv             # Original data
├── scripts/
│   └── kms_analysis.sql           # All SQL queries used
├── images/
│   ├── flat-file-import.png
│   ├── region-sales-chart.png
│   ├── customer-segmentation.png
│   └── shipping-analysis.png
```

---

## 8. 🧠 Skills Demonstrated

- ✅ SQL querying with GROUP BY, JOINS, and filtering
- ✅ Flat file import and data cleansing in SSMS
- ✅ Business problem-solving with real-world data
- ✅ Analytical thinking and recommendation writing
- ✅ SQL optimization and data type management

---

## 9. 🔗 Supporting Resources


![My Screenshot](https://drive.google.com/uc?export=view&id=1nQG90C0fMXsUYnjEb1Sg82l3tYJn4yez)

  

---

## 10. 🙋‍♂️ About Me

**Esther Olutomisin Faloore**  
Aspiring Data Analyst passionate about using data to solve business problems and deliver impact through SQL, Excel, and PowerBI.

- 
- 📧 Email: estheroluwatomisin1@gmail.com

