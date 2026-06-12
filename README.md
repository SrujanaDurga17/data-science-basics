#PANDAS
Numpy = math engine - arrays (numbers only)
Pandas= data brain - real world data (rows and columns)

Pandas- used to work with structured data-csv,excel,sql tables (tables)
Load data (Pandas)
Clean data (Pandas)
Convert to NumPy
Train model

Importing Pandas: import pandas as pd
 Core Structure: DataFrame (rows+columns)
 Creating a dataframe- 
import pandas as pd
data={“Name”:[“Srujana”,”Rahul”],
	“Age”:[25,26],
	“Salary”: [50000,60000]
df=pd.DataFrame(data)
Series Vs DataFrame
 series= single column, dataframe = full table
Reading csv and basic operation-
data=pd.read_csv(“filepath”)
data.head()  #returns the first 5 rows
data.tail()  #returns last 5 rows
data.info() #returns datatypes, missing values
data.shape #give the number of rows and columns
Selecting Columns-
	     a. data[“Name”] # get single column
	     b. data[“Name”,”Age”] # two columns
Filtering data-
df[df[“Age”] >25] # only rows >25
No condition - df[~(df["Age"] > 25)] 
MULTIPLE CONDITIONS
AND - df[(df[“Age”]>25 &df[”Salary”]>30000)]
OR- df[(df[“Age”]>25 | df[“Salary”] >30000)]
	      d.Using .isin – df[df[“Name”].isin([“Srujana”,”Rahul”])]
	      e. Between – df[df["Age"].between(20, 30)]
	      f.  String filtering  –
 i.  df[df[“Name”].str.contains(“rah”)]
ii. df[df["Name"].str.startswith("S")]
iii. df[df["Name"].str.endswith("a")]
      7. Adding new column- 
 Add a column with a constant value- df['C'] = 100
Add a column with a list of values (must match the DataFrame length)- df['D'] = [5, 6]
Add a calculated column derived from existing columns - df['E'] = df['A'] + df['B'] 
      8.  Missing Values
	Df.isnull –df[df["Salary"].isnull()]
	df.dropna()
	df.fillna(0)
	df.notnull() –df[df["Salary"].notnull()]
      9. Drop column:
df.drop([“Col1”,”col2”],axis=1)
axis=1 ->works for columns
ais=0 for rows
     10. inplace — Whether to modify the original DataFrame
inplace=False (default)
Returns a new DataFrame and leaves the original unchanged.
new_df = df.drop("Age", axis=1)df is unchanged.
inplace=True
Modifies the existing DataFrame directly.
df.drop("Age", axis=1, inplace=True)
   Parameter
Purpose
Example
axis=0
Work on rows
df.drop(0, axis=0)
axis=1
Work on columns
df.drop("Age", axis=1)
inplace=True
Modify original DataFrame
df.drop("Age", axis=1, inplace=True)
inplace=False
Return a new DataFrame
new_df = df.drop("Age", axis=1)

 Filtering example -df[
(df["Age"] > 25) &
(df["Salary"] > 50000) &
(df["Name"].str.startswith("S"))]

Expression
Output
df["Age"] > 25
True/False mask
df[df["Age"] > 25]
filtered table


Groupby-

import pandas as pd
df = pd.DataFrame({
    "Name": ["Srujana", "Rahul", "Asha", "Kiran", "Sita", "Arjun"],
    "Dept": ["IT", "HR", "IT", "Finance", "IT", "HR"],
    "Salary": [50000, 60000, 45000, 70000, 52000, 80000]
})
df.groupby("Dept")                 -This alone does nothing visible ,We must apply aggregation.

Mean- df.groupby("Dept")["Salary"].mean()
Output- 
Finance    70000
HR         70000
IT         49000
Name: Salary, dtype: int64

Sum- df.groupby(“Dept”)[“Salary”].sum()

Count- df.groupby(“Dept”)[“Name”].count()



Aggregate 
df.groupby("Dept")["salary"].agg(["mean","max","min","sum"])

Multiple group by-
df.groupby(["Dept","Name")["salary"].sum()
 

Merging/Joining Dataframes - Merging two tables which have a common column

Inner join - Only matching rows:
inner = pd.merge(customers, orders, on='customer_id', how='inner') 

Left Join- all customers,orders where available
left = pd.merge(customers, orders, on='customer_id', how='left')
print(left)

Right Join- all orders, customers where available
right = pd.merge(customers, orders, on='customer_id', how='right')
print(right)

Outer join - keeps everything
outer = pd.merge(customers, orders, on='customer_id', how='outer') 

Join()- Merge on index - use when the join key is the dataframe’s index

df1 = customers.set_index('customer_id')
df2 = orders.groupby('customer_id') 'amount'.sum()

df1.join(df2)






