# 🥝 Sales Data Analysis – Handling Missing Prices & Revenue Calculation

## 📌 Project Overview
This project analyzes a small sales dataset where **some orders are missing the `unit_price`**.  
The main objective is to **clean the data**, **fill missing values intelligently**, and **calculate total revenue**, followed by basic data exploration and visualization.
---



## 🎯 Problem Statement

Some of the orders are missing the `unit_price`.


### Your Tasks:

1. Fill in each missing `unit_price` using the **average price of the same product**
2. Calculate **total price per order**
3. Calculate **total revenue across all orders**
4. Perform basic data exploration and visualization
5. Answer business questions using Python
---



## 🧰 Tools & Technologies

- Python 3
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
---



## 📂 Dataset Columns

- `order_id`
- `customer_name`
- `product`
- `quantity`
- `unit_price`
- `order_date`
---


## 🧪 Steps in Jupyter Notebook


### 1️⃣ Importing Libraries & Reading Data

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv("kiwilytics_orders.csv")
```

---


### 2️⃣ Exploring the Dataset

```
df.head()
df.info()
df.describe()
```

---

<ins>Goals:</ins>
* Understand data types
* Identify missing values
* Review basic statistics



### 3️⃣ Handling Missing Data

Some **unit_price** values are missing.

**Strategy:**
Fill missing prices using the **average unit price per product.**

```
# Fill missing unit_price with average price per product
df['unit_price'] = df['unit_price'].fillna(
    df.groupby('product')['unit_price'].transform('mean')
)
```


> [!NOTE] This ensures consistency
> [!NOTE] Avoids hard-coding values
> [!NOTE] Scales well for large datasets

### 4️⃣ Convert Data Types

> Convert date columns to datetime

```
# df['order_date'] = pd.to_datetime(df['order_date'])
```

> Convert float columns to float

```
# df['order_id'] = pd.to_numeric(df['order_id'])
# df['quantity'] = pd.to_numeric(df['quantity'])
# df['unit_price'] = pd.to_numeric(df['unit_price'])
```

### 5️⃣ Calculate Total Price & Revenue

> Total price per order

```
df['unit_price'] = df['unit_price'].fillna(
    df.groupby('product')['unit_price'].transform('mean')
)

# Calculate total price per order
df['total_price'] = df['quantity'] * df['unit_price']
```

> Total revenue across all orders

```
# Calculate total revenue
total_revenue = df['total_price'].sum()

total_revenue
```

✅ Final Answer:
> Total Revenue = 1167.5

### 6️⃣ Data Visualization (Matplotlib)

> Plot the Highest Total Quantity Sold per Product

```
HighestTotalQuantitySold = df.groupby('product', sort=True)["quantity"].sum().reset_index(name ='Total Quantity')
HighestTotalQuantitySold
```


### 7️⃣ Business Question

> [!CAUTION] Which customer has the highest total spending across all orders?

```
HighestTotalSpendingSold = df.groupby('customer_name', sort=False)["quantity"].sum().nlargest(5).reset_index(name ='Total Spending')

HighestTotalSpendingSold
```

```
fig, ax = plt.subplots()

x = HighestTotalQuantitySold['product']
y = HighestTotalQuantitySold['Total Quantity']


# ax.bar(x, y, label=bar_labels, color=bar_colors)
ax.bar(x, y)

ax.set_xlabel('Product Name')
ax.set_ylabel('Total Quantity')

ax.set_title('The highest total quantity sold')
ax.legend()

plt.show()
```


#### 🏆 Answer:

The customer with the highest total spending is:

> Eric


#### 📈 Key Learnings


* Handling missing data using **group-based averages**
* Vectorized calculations with Pandas
* Revenue analytics fundamentals
* Simple yet effective data visualization
* Answering real business questions using data



### 🚀 Possible Extensions

* Daily / Monthly revenue analysis
* Store cleaned data into PostgreSQL
* Build an ETL pipeline
* Add Seaborn visualizations
* Scale for large datasets


### 👤 Author


Moustafa Gaber

Data • Analytics • ETL • Python

