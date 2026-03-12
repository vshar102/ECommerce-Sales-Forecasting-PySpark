# ECommerce-Sales-Forecasting-PySpark

## 📌 Project Overview
Online shopping has rapidly evolved, providing immense convenience to customers but presenting complex logistical challenges behind the scenes. Uncertainty plays a significant role in how supply chains plan operations, often leading to stockouts, delayed deliveries, and increased operational costs.

This project focuses on leveraging **Apache Spark (PySpark)** and Machine Learning to forecast product sales for a multinational e-commerce company. By predicting future demand, the Sales & Operations Planning (S&OP) team can strategically manage inventory, plan promotions, and ensure customer satisfaction with prompt deliveries during high-demand periods like end-of-the-year sales.

## 🎯 Business Objective
* **Demand Forecasting:** Predict the daily quantity of products sold to optimize inventory management.
* **Supply Chain Optimization:** Minimize uncertainties related to stockouts and overstocking.
* **Strategic Planning:** Assist the S&OP team in planning for end-of-year sales and promotions.

## 🛠️ Technology Stack
* **Language:** Python 3
* **Big Data Framework:** Apache Spark (PySpark)
* **Machine Learning:** PySpark MLlib (`RandomForestRegressor`, `Pipeline`, `VectorAssembler`, `StringIndexer`)
* **Environment:** Jupyter Notebook

## 📊 Dataset Description
The dataset (`Online Retail.csv`) contains transactional data uniquely identifying purchases, products, and customers.

| Feature         | Description |
|-----------------|-------------|
| `InvoiceNo`     | A 6-digit number uniquely assigned to each transaction |
| `StockCode`     | A 5-digit number uniquely assigned to each distinct product |
| `Description`   | The product name |
| `Quantity`      | The quantity of each product (item) per transaction |
| `UnitPrice`     | Product price per unit |
| `CustomerID`    | A 5-digit number uniquely assigned to each customer |
| `Country`       | The name of the country where each customer resides |
| `InvoiceDate`   | Date and time when the transaction was generated (`d/M/yyyy H:mm`) |
| `Year`, `Month`, `Week`, `Day`, `DayOfWeek` | Time-based extracted features for analysis |

## ⚙️ Project Workflow

1. **Data Ingestion & Formatting:** 
   * Initialized a Spark session.
   * Loaded the `Online Retail.csv` dataset using PySpark.
   * Converted `InvoiceDate` strings into proper timestamp and date formats.
2. **Data Aggregation & Feature Engineering:**
   * Grouped raw transactional data into **daily intervals** by country and product (`StockCode`).
   * Aggregated features: calculated Total Quantity sold and Average Unit Price.
3. **Data Splitting:**
   * Split the dataset into training and testing sets based on a cutoff date (`2011-09-25`) to simulate real-world forecasting (training on past data, evaluating on future data).
4. **Machine Learning Pipeline Construction:**
   * **Categorical Encoding:** Applied `StringIndexer` to encode categorical variables (`Country`, `StockCode`).
   * **Vector Assembly:** Consolidated all predictive features (`CountryIndex`, `StockCodeIndex`, `Month`, `Year`, `DayOfWeek`, `Day`, `Week`) into a single feature vector using `VectorAssembler`.
   * **Model Selection:** Implemented a `RandomForestRegressor` with optimized bins (`maxBins=4000`) to handle high cardinality in stock codes.
   * **Pipeline:** Bundled indexers, the assembler, and the model into a unified PySpark `Pipeline` for streamlined training and inference.
5. **Model Evaluation & Predictions:**
   * Evaluated model performance on the test set using **Mean Absolute Error (MAE)**.
   * Extracted specific business insights, such as forecasting the total units sold during promotional week 39 of 2011.

## 📈 Key Findings
Through distributed machine learning pipelines built entirely via PySpark, this repository demonstrates robust demand forecasting capable of processing extensive e-commerce datasets efficiently, providing actionable supply chain intelligence.
