# Walmart-Data-Analysis-Supply-Chain.
1. Data Import
You began by importing necessary libraries (pandas, numpy, seaborn, matplotlib) and reading three datasets:
train_walmart.csv: Contains training data on weekly sales.
stores.csv: Contains store-level information.
features.csv: Contains additional features such as temperature, fuel prices, and holidays.

2. Data Exploration and Cleaning
Initial Exploration:
Checked the first few rows of features and stores using .head().
Inspected missing values with .isnull().sum().
Feature Cleaning:
Dropped unnecessary markdown columns (MarkDown1-5) using .drop() since they were not required.
Handled missing values in the features dataset by forward-filling with .fillna(method='ffill').

3. Merging Datasets
To create a unified dataset for analysis:
Merged train_walmart.csv and stores.csv on the Store column.
Further merged the resulting dataset with features.csv on Store, Date, and IsHoliday.

4. Date-Time Transformation
Converted the Date column to a datetime object using pd.to_datetime().
Extracted additional features:
Year (df['year']).
Week (df['week']), using .dt.isocalendar().

5. Scatter Plot Function
You created a function scatter(column) to visualize relationships between any feature and Weekly_Sales:
Example: scatter('Store') and scatter('Size').

6. Trend Analysis: Weekly Sales by Year
Grouped weekly sales data by year and week, then calculated average sales for each week.
Visualized the trends with sns.lineplot for 2010, 2011, and 2012, using:
Green for 2010 and 2011.
Blue for 2012.
Finalized with a combined line chart for all years and added labels, legends, and grid.

7. Distribution of Weekly Sales
Visualized the distribution of Weekly_Sales using sns.distplot().

8. Store-Level Analysis
Computed average weekly sales for each store using .groupby(['Store'])['Weekly_Sales'].mean().
Sorted and visualized:
Bar plot for average weekly sales per store (sns.barplot).
Highlighted the stores with highest and lowest average sales.

9. Department-Level Analysis
Calculated average weekly sales per department using .groupby('Dept').
Sorted and visualized the data:
Bar plot for weekly sales by department.
Highlighted departments with highest and lowest average sales.

10. Correlation Heatmap
Analyzed relationships among numerical features using sns.heatmap(df.corr(), annot=True).

11. Category Analysis
Store Type: Analyzed average weekly sales across store types (Type) using .groupby() and bar plots.
Store Size: Used sns.boxplot to visualize the size distribution across store types.

12. Unemployment and Sales Trends
Analyzed the sum of unemployment by year with .groupby(['year'])['Unemployment'].sum().plot().
Plotted the yearly average of weekly sales to observe trends over time.
Evaluated the frequency of holidays per year using .groupby(['year'])['IsHoliday'].sum().plot().

13. Department Unemployment Analysis
Explored the sum of unemployment by department:
Identified top 10 departments with lowest and highest unemployment using .sort_values() and bar plots.


![image](https://github.com/user-attachments/assets/c48d4128-1df7-449f-91bd-696ead1059c0)
![image](https://github.com/user-attachments/assets/b73296c0-a5d7-48e2-b055-2cd1e63092b2)
![image](https://github.com/user-attachments/assets/57f04b10-0413-42a8-b3b8-55b4b5b1060e)
![image](https://github.com/user-attachments/assets/0984e90f-74b0-4a9f-95b2-5f0820a30cbf)
![image](https://github.com/user-attachments/assets/717c74f4-d97a-46fc-956c-11db96ec6fa9)
![image](https://github.com/user-attachments/assets/8bf59e41-54e7-4a53-adf4-04d5b490e48f)
![image](https://github.com/user-attachments/assets/40d67ca3-b431-40f1-a81c-aaab73cf066c)
![image](https://github.com/user-attachments/assets/980a3138-e6e3-4446-9fa0-ee744085d7c9)
![image](https://github.com/user-attachments/assets/3800a89b-b12b-4299-be2b-dde81d5ecd87)
![image](https://github.com/user-attachments/assets/49cdef5f-01cc-4064-9dc5-5afbf4fc0a6c)
![image](https://github.com/user-attachments/assets/48ec7597-33cc-4209-a6d7-875c9b5b7c9d)
![image](https://github.com/user-attachments/assets/e0cd4ea2-6af8-4557-95a7-dae08dcb6338)











