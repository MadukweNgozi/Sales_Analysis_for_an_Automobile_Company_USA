# Sales_Analysis_for_an_Automobile_Company_USA
A Data Science Project that Analysed  the sales performance of an Automobile company Based in the United States. The company’s sales transaction data generated over the past years was used for this  analysis.

## PROBLEM STATEMENT:  
What are the Top Most-Profitable 5 States for the Bike Product Category business in the United State ?

## DATA PRE-PROCESSING

#### DATA LOADING
##  Importing all the necessary python packages 
```Python

# Solution

import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt

print("The packages have been successfull imported")

```


```Python
# Reading the sales data into a pandas dataframe 

bikes_df = pd.read_csv("C:/Users/Mazeliz Depot1/Desktop/NGOZI/_Mr Emma class/Data Set/bikes.csv")
bikes_df.head()    
```

## Data Modification
```Python
# (1). Adding the following 3 columns to your pansdas Dataframe:  bikes_df



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
```Python
### Filtering out only the data relevant to solving the problem statement

Is_US =   bikes_df["CustomerCountry"] == "United States"
Is_bike = bikes_df["ProductCategory"] == "Bikes"
bike_in_US = bikes_df[(Is_US) & (Is_bike)]
bike_in_US.head()
```
#### Data Aggregation / Data Summary
```Python
#Aggregating the total profit by states in the United State for bike sales

Total_profit_by_states = bike_in_US.pivot_table(values = "Profit", index = "CustomerState", aggfunc = np.sum)
Total_profit_by_states
```

#### DATA SORTING
```Python
# Sorting the Aggregated data to rank the the result(state) according to the top most profitable state 

Total_profit_by_states.sort_values("Profit", ascending = False)
```



