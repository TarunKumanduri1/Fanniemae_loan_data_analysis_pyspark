# **Fannie Mae Single Family Load Data Analysis using PySpark**

## **Overview**
This project analyzes loan performance, borrower characteristics, delinquency trends, credit risk factors, and property price variations using **PySpark** and **Pandas** in Google Colab. The dataset is sourced from **Single Family loan data from Fannie Mae** for 2010 and 2011. The analysis focuses on **loan default rates, borrower FICO scores, delinquency trends, and property price changes**.

The data is processed and stored in **Parquet format** for efficient querying and manipulation.

## **Data Sources**
- Mortgage loan data for 2010 and 2011 (Processed using **PySpark**)
- Data is stored in Google Drive under the directory: `/content/drive/MyDrive/Big_Data/Project_1/Data/`

## **Project Objectives**
- **Analyze FICO Score Trends** (Comparing borrower and co-borrower credit scores across years)
- **Study Delinquency Rates** (How loan delinquency varies over time and across loan terms)
- **Evaluate Credit Score Distribution** (Assess the creditworthiness of first-time buyers by state)
- **Measure Correlation of Loan Risk Factors** (FICO Score, LTV Ratio, and Interest Rate correlation with loan performance)
- **Visualize Loan Performance Trends** (Comparing default rates across different quarters)
- **Examine Loan Recovery Rates** (Percentage of loan recovered after default)
- **Assess Property Price Fluctuations** (Variation in property prices over time)

---

## **1. Data Processing**
The data from **2010 and 2011** is read and stored in **Parquet format** for efficient querying:
- CSV files for each year (`2010/*.csv`, `2011/*.csv`) are **merged** into:
  - `/content/drive/MyDrive/Big_Data/Project_1/Data/2010/merged_2010.parquet`
  - `/content/drive/MyDrive/Big_Data/Project_1/Data/2011/merged_2011.parquet`
- Column names are **renamed for clarity**, and datasets for both years are **combined**.

---

## **2. FICO Score Analysis**
- **Comparison of Borrower and Co-borrower FICO Scores (2010 vs 2011)**
- **Key Findings**:
  - The **average borrower FICO score** increased slightly from **764.38 (2010) to 765.43 (2011)**.
  - Co-borrowers had slightly **higher credit scores** than primary borrowers.
  - This indicates an **improving credit quality** of mortgage borrowers over time.

🔹 **Visualization**: A **bar chart** comparing borrower and co-borrower FICO scores in **2010 and 2011**.

---

## **3. Loan Delinquency Trends**
- **Analyzed monthly delinquency rates** (30, 60, and 90 days past due)
- **Grouped loans based on original term**:
  - **≤ 15 years**
  - **16-30 years**
- **Key Findings**:
  - Higher **delinquency rates** in early **2010 and 2011**.
  - Loans with **longer terms (16-30 years)** had higher delinquency rates.
  - The peak **delinquency rate** was observed in **May 2011**.

🔹 **Visualization**: **Stacked bar chart** showing **monthly delinquency rates** by loan term group.

---

## **4. Credit Score Distribution for First-Time Buyers**
- **Classified credit scores** into:
  - **Poor (<580)**
  - **Fair (580-669)**
  - **Good (670-739)**
  - **Very Good (740-799)**
  - **Excellent (800+)**
- **Key Findings**:
  - Most **first-time homebuyers** had **Very Good (740-799)** credit scores.
  - **No loans** were issued to borrowers with **Poor credit**.
  - **California (CA) and Texas (TX)** had the **highest share of Excellent credit borrowers**.

🔹 **Visualization**: **Stacked bar chart** showing the distribution of credit scores across U.S. states.

---

## **5. Correlation Analysis: FICO Score, LTV Ratio, Interest Rate vs Loan Status**
- **Analyzed correlations** between:
  - **FICO Score** and Loan Performance
  - **LTV Ratio** and Loan Status
  - **Interest Rate** and Loan Status
- **Key Findings**:
  - **Higher FICO Scores → Lower Loan Defaults**
  - **Higher LTV Ratio → Higher Interest Rates**
  - **Interest Rates had weak correlation with Loan Defaults**

🔹 **Visualization**: **Heatmap of correlation matrix** between loan factors.

---

## **6. Loan Performance & Credit Score Distribution**
- **Categorized loans** into:
  - **Performing Loans**
  - **Delinquent Loans (1-90 days past due)**
  - **Defaulted Loans (90+ days past due)**
- **Key Findings**:
  - **Defaulted loans** had significantly **lower FICO scores**.
  - Higher **LTV Ratios** were slightly linked to **higher default risk**.
  - **Higher interest rates** correlated with **higher defaults**.

🔹 **Visualization**: **Density plots** for **FICO Scores, LTV Ratios, and Interest Rates** by loan status.

---

## **7. Default Rate Trends Over Time**
- **Compared default rates by quarter** (2010 Q1 - 2011 Q4).
- **Key Findings**:
  - Default rates **peaked in 2011 Q2** (~0.70).
  - **2010 Q3 & 2010 Q4** had the **lowest default rates** (~0.44).
  - **Loan defaults declined in late 2011**, indicating an improving market.

🔹 **Visualization**: **Bar chart** of **default rate per quarter**.

---

## **8. Loan Recovery After Default**
- **Calculated loan recovery percentage** after foreclosure:
  - **Recovery Formula**:  
    `((UPB at Removal - Foreclosure Costs) / Original UPB) * 100`
- **Key Findings**:
  - **77.42% of the loan amount was recovered** after foreclosure.
  - **Foreclosure costs reduce recovery**, but most loans still retain significant value.

🔹 **Output**: **77.42% recovery rate**.

---

## **9. Property Price Variations Over Time**
- **Calculated monthly property price changes**:
  - `(Current List Price - Original List Price) / Original List Price * 100`
- **Key Findings**:
  - Data for **property price changes was unavailable** (null values).
  - **No valid dataset for price trends** in the mortgage records.

🔹 **Visualization**: **No plot due to missing data**.

---

## **How to Run the Code**
1. **Mount Google Drive** and **install PySpark**:
   ```python
   from google.colab import drive
   drive.mount('/content/drive')

   !pip install pyspark
   ```
2. **Load and Process Data**:
   ```python
   df = spark.read.csv(csv_path, header=False, sep="|", inferSchema=True)
   df.write.parquet(parquet_path, mode='overwrite')
   ```
3. **Perform Analysis**:
   - **Run FICO Score comparison**
   - **Calculate delinquency trends**
   - **Analyze loan performance**
   - **Visualize default rates over time**
   - **Check loan recovery after default**
   - **Analyze credit scores for first-time buyers**

---

## **Conclusion**
🔹 **Key Takeaways:**
- **FICO Scores improved slightly from 2010 to 2011**.
- **Longer loan terms (16-30 years) had higher delinquency rates**.
- **Higher LTV Ratios correlated with higher interest rates**.
- **Default rates peaked in 2011 Q2 but declined later**.
- **77.42% of loan amounts were recovered after default**.
- **Property price change data was unavailable**.

📊 **Final Recommendation**:
- **Encourage borrowers with strong FICO scores to secure lower interest rates**.
- **Implement risk-mitigation strategies for high-LTV loans**.
- **Continue monitoring delinquency trends to predict future loan risks**.

---

## **Author**
This project was developed using **PySpark** for **Big Data Loan Analysis**.
