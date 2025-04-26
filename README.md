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

![Pandas_Screenshot](https://github.com/user-attachments/assets/af9aa6da-77df-41df-b161-769936db2b10)



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
![Data_Modificatio](https://github.com/user-attachments/assets/7524d90e-b42a-429c-ad12-f141e4147e6d)


## DATA ANALYSIS
#### DATA FILTERING
```Python
### Filtering out only the data relevant to solving the problem statement

Is_US =   bikes_df["CustomerCountry"] == "United States"
Is_bike = bikes_df["ProductCategory"] == "Bikes"
bike_in_US = bikes_df[(Is_US) & (Is_bike)]
bike_in_US.head()
```
![Data Analysis Data Filtering](https://github.com/user-attachments/assets/9a55a24e-bcaa-465e-afb1-0eda9a8bc1a0)



#### Data Aggregation / Data Summary
```Python
#Aggregating the total profit by states in the United State for bike sales

Total_profit_by_states = bike_in_US.pivot_table(values = "Profit", index = "CustomerState", aggfunc = np.sum)
Total_profit_by_states
```

![Data Aggregation](https://github.com/user-attachments/assets/ed7f96a2-4dc0-47d9-8698-c6ff5c3d79a1)

#### DATA SORTING
```Python
# Sorting the Aggregated data to rank the the result(state) according to the top most profitable state 

Total_profit_by_states.sort_values("Profit", ascending = False)
```
![Data Sorting](https://github.com/user-attachments/assets/31ca38c1-1530-42e3-8886-a0d6c112735f)

#### RESULT 
```Python
# Top Most-Profitable 5 States for the Bike Product Category business
# in the United State
Top_5_most_profitable_states_US =Total_profit_by_states.sort_values("Profit", ascending = False).head()
Top_5_most_profitable_states_US
```

![Result](https://github.com/user-attachments/assets/d4909ef7-1411-4165-8bc9-8810afaa16c3)


## DATA VISUALIZATION
```Python

# Visualizaing the result

Top_5_most_profitable_states_US.plot(kind = "bar")

# Adding the title and label to the plot
plt.title("The Top 5 Most Profitable States For Bike Product in the US")

plt.ylabel("Total Profit in Million Dollars")
plt.xlabel("States")

# Showing the plot
plt.show
```

![Project_1_Screenshot](https://github.com/user-attachments/assets/a6c37b35-c2f4-4095-bde3-1ea067fdc5cd)
