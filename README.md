# 📊 Sales-Analytics-PowerBI
This project showcases the end-to-end process of building a Power BI dashboard for sales analysis using MySQL as the data source. It follows a structured project management approach using the AIMS Grid framework and simulates a real-world business scenario at AtliQ Hardware.

## 🛠 Tools Used
Power BI (Desktop)

MySQL 9.3 (via Workbench)

DAX (Data Analysis Expressions)

## 🔗 Data Source
MySQL relational database
Files: db_dump_version_2.sql

## 💡 Key Features
#### 📈 Interactive line and bar charts for year-wise and category-wise sales

#### 📊 Cards showing:

  -Total Revenue
    
   -Total Quantity Sold

   -Total Profit Margin

#### 🔄 Year slicer for dynamic filtering across all visuals

#### 🧠 Calculated columns and DAX measures:

  -Total Revenue

  -Total Quantity Sold

  -Total Profit Margin

#### 💵 Currency normalization for USD and INR values

## ⚙️ What I Learned
Performing ETL (Extract, Transform, Load) within Power BI

Creating dynamic visuals using slicers and filters

Writing DAX measures and fixing filter context issues

Importing updated SQL dumps and troubleshooting schema changes

## 🔗 Data Source and Flow
  -MySQL database loaded into Power BI

ETL steps performed inside Power BI:

  -Data cleaning

  -Currency normalization

  -Column renaming

Dataset includes INR and USD transactions from multiple global markets
