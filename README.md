```python
import pandas as pd
import os
import numpy as np
```


```python
pwd = os.getcwd()
```


```python
filepath = pwd + "/Unicorn_Companies.csv"
# filepath 
```




    'c:\\Users\\9ayus\\OneDrive\\Documents\\Projects\\Unicorns Worldwide/Unicorn_Companies.csv'




```python
unicorn = pd.read_csv(filepath)
```

Data Cleaning


```python
unicorn.rename(columns={"Select Inverstors": "Select Investors"},inplace=True)
```


```python
# checking the datatype

print(type("Company"))
print(type("Valuation ($B)"))
print(type("Date Joined"))
print(type("Country"))
print(type("City"))
print(type("Industry"))
print(type("Select Inverstors"))
print(type("Founded Year"))
print(type("Total Raised"))
print(type("Financial Stage"))
print(type("Investors Count"))
print(type("Deal Terms"))
print(type("Portfolio Exits"))
```

Correcting the datatype

Updating "Valuation ($B)" Column


```python
# Getting rid of ($)
# Converting datatype str to float
unicorn["Valuation ($B)"].replace({"\$": ""}, inplace=True)
unicorn["Valuation ($B)"] = unicorn["Valuation ($B)"].replace({"\$": " "}, regex=True)
unicorn["Valuation ($B)"] = unicorn["Valuation ($B)"].astype(float)
# unicorn
```

Updating "Date Joined" column


```python
# Converting datatype str to datetime
pd.to_datetime(unicorn["Date Joined"]) 
```

Updating "Total Raised" column


```python
# Getting rid of ($)
unicorn["Total Raised"] = unicorn["Total Raised"].replace({"\$": " "}, regex=True)

# Slicing ("B" and "M") from the str
new_total_raised = unicorn["Total Raised"].str[-1::]

# Adding new column and adding the value
unicorn["Total Raised in Billion or Million"] = unicorn["Total Raised"].str[-1::]

# Replacing the value 
unicorn["Total Raised in Billion or Million"].replace({"B": "Billion"}, inplace=True)
unicorn["Total Raised in Billion or Million"].replace({"M": "Million"}, inplace=True)

unicorn.rename(columns={"Total Raised": "Total Raised ($)"}, inplace=True)

#Getting rid of ("B" and "M") from total raised column
unicorn["Total Raised ($)"] = unicorn["Total Raised ($)"].map(lambda x: x.rstrip("BM"))
# unicorn

# Replacing values
# Converting datatype from str to float
unicorn["Total Raised ($)"] = unicorn["Total Raised ($)"].replace({"None": "0"}, inplace=True)
unicorn["Total Raised ($)"] = unicorn["Total Raised ($)"].astype(float)
# unicorn 
```

Updating "Investors count" column


```python
# Replacing values
# Converting datatype from str to float
unicorn["Investors Count"] = unicorn["Investors Count"].replace({"None": "0"}, regex=True)
unicorn["Investors Count"] = unicorn["Investors Count"].astype(float)
# unicorn 
```

Updating "Industry" column


```python
# Checking for unique values
unicorn["Industry"].value_counts().reset_index()

# Replacing the value
unicorn.replace({"Artificial Intelligence": "Artificial intelligence", "Finttech": "Fintech"}, inplace=True)
unicorn["Industry"].value_counts().reset_index() 
```

Updating "Deal Terms" column


```python
# Checking the unique value and replacing them
# Converting datatype from str to float
unicorn["Deal Terms"].unique() 
unicorn["Deal Terms"] = unicorn["Deal Terms"].replace({"None": "0"})
unicorn["Deal Terms"] = unicorn["Deal Terms"].astype(float) 
```


```python
# Checking for unique values
unicorn["Portfolio Exits"].value_counts().reset_index()

# Replacing values
# Converting datatype from str to float
unicorn["Portfolio Exits"] = unicorn["Portfolio Exits"].replace({"None": "0"},)
unicorn["Portfolio Exits"] = unicorn["Portfolio Exits"].astype(float) 
```


```python
# Checking the number of unique contries
unicorn["Country"].value_counts().reset_index()
```
