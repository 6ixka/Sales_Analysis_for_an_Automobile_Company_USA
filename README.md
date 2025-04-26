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

![data loading_ss](https://github.com/user-attachments/assets/adec9cb5-5925-4cfc-8180-9a5b5b9db97e)
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
![Data modification_ss](https://github.com/user-attachments/assets/720bf4cb-a118-4d2b-8924-0a5f67481bab)


## DATA ANALYSIS 

#### DATA FILTERING

```
# Filtering out only the data relevant to solving the problem statement

is_USA = bikes_df["CustomerCountry"] == "United States"
is_bike = bikes_df["ProductCategory"] == "Bikes"
bike_in_US = bikes_df[(is_USA) & (is_bike) ]
bike_in_US.head()
```
![Data filtering_ss](https://github.com/user-attachments/assets/7418957a-45f3-4d10-8b62-a936e7b89dc0)




#### DATA AGGREGATION 

```
# aggregating the total profit in the United States for bike sales

total_profit_by_states = bike_in_US.pivot_table(values = "Profit" , index = "CustomerState" , aggfunc = np.sum)
total_profit_by_states
```
![Data aggregation_ss](https://github.com/user-attachments/assets/48ae55cd-7a7d-46fa-974c-785be625619f)





#### DATA SORTING

```
# Sorting the aggregated data in order to rank the state according to the top most profitable states
total_profit_by_states.sort_values("Profit", ascending = False)
```
![Data Sorting_ss](https://github.com/user-attachments/assets/fb288b06-fb78-4788-bdc1-fc4be3fb327f)

#### RESULT

```
# The Top Most-Profitable 5 States for a Bike business in the United State 
top_most_profitable_5_states_US = total_profit_by_states.sort_values("Profit", ascending = False).head()
top_most_profitable_5_states_US
```
## DATA VISUALIZATION 
```
# Vissualizing the result

top_most_profitable_5_states_US .plot(kind = "bar")

# adding a a title and label to the plot

plt.title("The Top Most-Profitable 5 States for a Bike business in the United State")

plt.ylabel("Total Profit in Million Dollars")
plt.xlabel("States")

# showing the plot

plt.show
```

![image](https://github.com/user-attachments/assets/8329c5e8-5824-4d76-930b-eced7a0c11f2)











