\# 🥝 Sales Data Analysis – Handling Missing Prices \& Revenue Calculation



\## 📌 Project Overview

This project analyzes a small sales dataset where \*\*some orders are missing the `unit\_price`\*\*.  

The main objective is to \*\*clean the data\*\*, \*\*fill missing values intelligently\*\*, and \*\*calculate total revenue\*\*, followed by basic data exploration and visualization.



---



\## 🎯 Problem Statement

Some of the orders are missing the `unit\_price`.



\### Your Tasks:

1\. Fill in each missing `unit\_price` using the \*\*average price of the same product\*\*

2\. Calculate \*\*total price per order\*\*

3\. Calculate \*\*total revenue across all orders\*\*

4\. Perform basic data exploration and visualization

5\. Answer business questions using Python



---



\## 🧰 Tools \& Technologies

\- Python 3

\- Jupyter Notebook

\- Pandas

\- NumPy

\- Matplotlib



---



\## 📂 Dataset Columns

\- `order\_id`

\- `customer\_name`

\- `product`

\- `quantity`

\- `unit\_price`

\- `order\_date`



---



\## 🧪 Steps in Jupyter Notebook



\### 1️⃣ Importing Libraries \& Reading Data

```python

import pandas as pd

import numpy as np

import matplotlib.pyplot as plt



df = pd.read\_csv("kiwilytics\_orders.csv")

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



\### 3️⃣ Handling Missing Data



Some `***unit\_price`*** values are missing.



**Strategy:**



Fill missing prices using the **average unit price per product.**

```

df\['unit\_price'] = df\['unit\_price'].fillna(

&nbsp;   df.groupby('product')\['unit\_price'].transform('mean')

)

```



> \[!NOTE] This ensures consistency

> \[!NOTE] Avoids hard-coding values

> \[!NOTE] Scales well for large datasets



\### 4️⃣ Convert Data Types



> Convert date columns to datetime



```

df\['order\_date'] = pd.to\_datetime(df\['order\_date'])

```



> Convert float columns to float

```

df\['unit\_price'] = df\['unit\_price'].astype(float)

```



\### 5️⃣ Calculate Total Price \& Revenue



> Total price per order

```

df\['total\_price'] = df\['quantity'] \* df\['unit\_price']

```



> Total revenue across all orders

```

total\_revenue = df\['total\_price'].sum()

total\_revenue

```



✅ Final Answer:



> Total Revenue = 1167.5



\### 6️⃣ Data Visualization (Matplotlib)



> Plot the Highest Total Quantity Sold per Product



```

product\_quantity = df.groupby('product')\['quantity'].sum()



product\_quantity.plot(

&nbsp;   kind='bar',

&nbsp;   title='Total Quantity Sold per Product'

)



plt.xlabel('Product')

plt.ylabel('Total Quantity Sold')

plt.show()

```



\### 7️⃣ Business Question

> \[!CAUTION] Which customer has the highest total spending across all orders?

```

customer\_spending = df.groupby('customer\_name')\['total\_price'].sum()



customer\_spending.sort\_values(ascending=False).head(1)

```



\#### 🏆 Answer:



The customer with the highest total spending is:

> Eric



\#### 📈 Key Learnings



* Handling missing data using \*\*group-based averages\*\*
* Vectorized calculations with Pandas
* Revenue analytics fundamentals
* Simple yet effective data visualization
* Answering real business questions using data



\### 🚀 Possible Extensions



* Daily / Monthly revenue analysis
* Store cleaned data into PostgreSQL
* Build an ETL pipeline
* Add Seaborn visualizations
* Scale for large datasets



\### 👤 Author



Moustafa Gaber

Data • Analytics • ETL • Python

