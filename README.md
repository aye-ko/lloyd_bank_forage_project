# Lloyd Bank EDA

## Project Overview

***Objective***: First Critical Steps to build a predictive model for customer churn.  Gather all relevant data, then conduct an EDA and prepare the dataset for model development. 

### BOTTOM LINE UP FRONT:
-	Churn Rate: 20%
-	There is no clear correlation between any of the metrics and churn status, indicating that it is probably a combination of factors. 
-	Through Clustering, we find our second-highest spenders have the highest churn rate at 27%. Cluster 6, our top spenders, churns at 21%. Our most valuable customers are leaving at higher rates than average (20.4% overall churn). The reason remains undetermined due to low feature correlation. Further investigation is required

### Business Problem: 
We need to predict which of our customers are likely to churn. 

### Goal: 
Conduct exploratory data analysis and translate the findings into a predictive model that identifies which customers are likely to churn. 

### Methodology and Justification
***Tools Used***:
Python for data cleaning, manipulation, analysis, and visualization
Reason: Python has libraries that are suited for the assignment. Pandas is used for date manipulation, numpy for calculations, matplotlib and seaborn for data visualization, sklearn for machine learning models, and datetime for calculating date ranges in days. 

### Identifying and Gathering Steps:
-	Downloaded the data from the Excel files and uploaded a copy using pd.read_excel, as it is an Excel file.
-	Kept the names the same as the sheets for consistency across the board. 
-	Printed the head of each Sheet and compared it to the original dataset for accuracy and to ensure consistency, and that nothing is lost

### Data Cleaning Process
-	Steps taken to ensure data integrity:
-	Created a backup of the original raw data
-	Created a Transaction_Summary based on Transaction_History, grouped by CustomerID to create a single column per customer rather than multiple columns.
-	Grouped by minimum and Maximum transaction, the number of transactions, and the total spent per customer, and also calculated the LoyaltyLength by subtracting the most recent transaction date from the first transaction date. 

All these are new columns that are added to a table and dropped all null values from Transaction_Summary I don’t need to analyze customers who haven’t spend any money. 
***Documentation:*** All cleaning steps are documented with inline comments.
-	For the Customer_Service, and InteractionType, I created unique columns again to make sure there is one column per CustomerID as it has a one to many relationship with InteractionType. 1 customer can put in multiple Interaction or have none,  The summary dataframe groups it by feedback, inquiry or complaint and if it was resolved or not each has its own columns assigned to that customer. 
-	For customers with no values, the Nan are filled with zero rather than dropping the column
-	For customers with no demographics, churn status, or online activity, their Nan Values were dropped. 
-	The result was that we started with 1000 rows and ended up with 1000 rows. 
-	Customer_Data is a new table that groups all these tables and columns using a merge and inner join for the Churn_Status and the Demographics on the CustomerID because they are the key placeholders. Then a left join with Transaction_Summary, Customer_Service_Summary, and the Online_Activity.

### Analysis Steps:
1.	Descriptive Statistics
-	Used the  describe().T function to calculate mean, median, standard deviation, minimum, 25% quartile, median 75% quartile, maximum, and then the skew and kurtosis as well for all numeric variables. 
-	Calculated skew and kurtosis to determine distribution shapes, and see where the outliers mostly are, and to determine where to use StandardScale or RobustScale when calculating z scores.
-	Calculated the churn rate to check for balance.  


2. Relationship Analysis
- Correlation analysis between numeric values and churn_rate

3. Customer Segmentation
- Standardized all numeric features using z-scores
- Applied k-means clustering (k=9) to identify natural customer groups

### Data Source

Dataset: Customer Churn Data
Source:  Forage Assignment

Data Quality Assessment (ROCCC):
- Reliable: Direct from mock company data
- Original: First-party company data
- Comprehensive: Contains all necessary variables for analysis
- Current: Static dataset (not real-time)
- Cited:  Well-documented source

Limitations:
- Data does not indicate if feedback is positive or negative, which is a valid metric in measuring which customers churn. 
- Data is not dynamic/real-time
- Limited to a point-in-time snapshot


Author
Onyedikachukwu Okonkwo


