# Sales_Analysis_for_an_Automobile_Company_USA
A Data Science Project that Analysed  the sales performance of an Automobile company Based in the United States. The company’s sales transaction data generated over the past years was used for this  analysis.

## PROBLEM STATEMENT:  
What are the Top Most-Profitable 5 States for a Bike business in the United State ?

## DATA PRE-PROCESSING 
#### DATA LOADING
```Python
# importing all the necessary python packages 

# solution 

import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt

print("Packages successfully imported")


```



```Python
# reading the sales data into a pandas dataframe

# Solution

bikes_df =  pd.read_csv('C:/Users/Admin/Documents/_EXCLUSIVE DATA SCIENCE BOOT CAMP_STUDENT FOLDER/_DATASET/bikes.csv')
bikes_df.head()


```
#### DATA MODIFICATION 

```
# (1). Adding the following 3 columns to your pandas Dataframe:  bikes_df




# TotalCostPrice : To be obtained by (OrderQuantity x CostPrice_usd)


bikes_df["TotalCostPrice"] = bikes_df["OrderQuantity"] * bikes_df["CostPrice_usd"] 


# SalesRevenue : To be obtained by (OrderQuantity x SellingPrice_usd)


bikes_df["SalesRevenue"] = bikes_df["OrderQuantity"] * bikes_df["SellingPrice_usd"] 



# Profit : To be obtained by (SalesRevenue - TotalCostPrice)



bikes_df["Profit"] = bikes_df["SalesRevenue"] - bikes_df["TotalCostPrice"]


bikes_df.head()


```

## DATA ANALYSIS 

#### DATA FILTERING

```
# Filtering out only the data relevant to solving the problem statement

is_USA = bikes_df["CustomerCountry"] == "United States"
is_bike = bikes_df["ProductCategory"] == "Bikes"
bike_in_US = bikes_df[(is_USA) & (is_bike) ]
bike_in_US.head()
```

#### DATA AGGREGATION 
```
# aggregating the total profit in the United States for bike sales

total_profit_by_states = bike_in_US.pivot_table(values = "Profit" , index = "CustomerState" , aggfunc = np.sum)
total_profit_by_states
```
