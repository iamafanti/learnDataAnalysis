# learnDataAnalysis
This is the notebook for me to learn data science, especially for Pandas.
## 1. Getting started with Pandas

Why do I need study Pandas? Because there are some drawbacks about Numpy:

A. All of the items in an array must have the same data type. For many datasets, this can make arrays cumbersome to work with. 
B. Columns and rows must be referred to by number, which gets confusing when you go back and forth from column name to column number.

Pandas is an important tool in data scientists's toolset. Just as ndarray in Numpy, Pandas has **dataframe** to represent tabular data. 

One of the biggest advantages that pandas has over NumPy is the ability to store mixed data types in rows and columns. Many tabular datasets contain a range of data types and pandas dataframes handle mixed data types effortlessly while NumPy doesn't. Pandas dataframes can also handle missing values gracefully using a custom object, NaN, to represent those values. A common complaint with NumPy is its lack of an object to represent missing values and people end up having to find and replace these values manually. In addition, pandas dataframes contain axis labels for both rows and columns and enable you to refer to elements in the dataframe more intuitively. Since many tabular datasets contain column titles, this means that dataframes preserve the metadata from the file around the data.

### Import Pandas

Before use Pandas, we must imprt it to the python environment by typing in:

`import pandas`

### Get in CSV files

To read a CSV file into a dataframe, we use the `pandas.read_csv()` function and pass in the file name as a string:
```
# To read in the file `crime_rates.csv` into a dataframe named crime_rates.
crime_rates = pandas.read_csv("crime_rates.csv")
```
You can read more about the parameters the read_csv() method takes to customize how a file is read in on the [documentation page](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html).

### Exporing the Pandas dataframe
When you call `head()` method, pandas will return **a new dataframe** containing just the first 5 rows:
```
first_rows = food_info.head()
```
If you peek at the [documentation](http://pandas.pydata.org/pandas-docs/version/0.17.1/generated/pandas.DataFrame.head.html), you'll notice that you can pass in an integer (n) into the head() method to display the first n rows instead of the first 5:
```
# First 3 rows.
print(food_info.head(3))
```
Because this dataframe contains many columns and rows, pandas uses ellipsis (...) to hide the columns and rows in the middle. Only the first few and the last few columns and rows are displayed to conserve space.

To access the full list of column names, use the columns attribute:
```
column_names = food_info.columns
```
We can use tolist() function to change 'column_names'to a list.

Lastly, you can use the `shape` attribute to understand the dimensions of the dataframe. The `shape` attribute returns a tuple of integers representing the number of rows followed by the number of columns:
```
# Returns the tuple (8618,36) and assigns to `dimensions`.
dimensions = food_info.shape
# The number of rows, 8618.
num_rows = dimensions[0]
# The number of columns, 36.
num_cols = dimensions[1]
```

### Indexing
When you read in a file into a dataframe, pandas uses the values in the first row (also known as the header) for the column labels and the row number for the row labels. Collectively, the labels are referred to as the index. dataframes contain both a row index and a column index.

### Series
The **Series** object is a core data structure that pandas uses to represent rows and columns. A Series is a labelled collection of values similar to the NumPy vector. The main advantage of Series objects is the ability to utilize non-integer labels. NumPy arrays can only utilize integer labels for indexing.

Pandas utilizes this feature to provide more context when returning a row or a column from a dataframe. For example, when you select a row from a dataframe, instead of just returning the values in that row as a list, pandas returns a Series object that contains the column labels as well as the corresponding values:
![avatar](images/series.png)



### Selecting a row

In Pandas, we use method `loc[]` to select rows from a dataframe. If you're interested in accessing a single row, pass in the row label to the loc[] method. Python will return an error if you don't pass in a valid row label:
```
# Series object representing the row at index 0.
food_info.loc[0]

# Series object representing the seventh row.
food_info.loc[6]

# Will throw an error: "KeyError: 'the label [8620] is not in the [index]'"
food_info.loc[8620]
```
When accessing an individual row, pandas returns a Series object containing the column names and that row's value for each column.

### Data Types
<ul>
    <li>object - for representing string values.</li>
    <li>int - for representing integer values.</li>
    <li>float - for representing float values.</li>
    <li>datetime - for representing time values.</li>
    <li>bool - for representing Boolean values.</li>
</ul>
When reading a file into a dataframe, pandas analyzes the values and infers each column's types. To access the types for each column, use the DataFrame.dtypes attribute to return a Series containing each column name and its corresponding type. Read more about data types on the Pandas documents.

If you're interested in accessing multiple rows of the dataframe, you can pass in either a slice of row labels or a list of row labels and pandas will return a dataframe. 
*Attention: Note that unlike slicing lists in Python, a slice of a dataframe using .loc[] will include both the start and the end row*:
```
# DataFrame containing the rows at index 3, 4, 5, and 6 returned.
food_info.loc[3:6]

# DataFrame containing the rows at index 2, 5, and 10 returned. Either of the following work.
# Method 1
two_five_ten = [2,5,10] 
food_info.loc[two_five_ten]

# Method 2
food_info.loc[[2,5,10]]
```
### Selecting column
When accessing a column in a dataframe, pandas returns a Series object containing the row label and each row's value for that column. To access a single column, use bracket notation and pass in the column name as a string:
```
# Series object representing the "NDB_No" column.
ndb_col = food_info["NDB_No"]

# You can instead access a column by passing in a string variable.
col_name = "NDB_No"
ndb_col = food_info[col_name]
```
To select multiple columns, pass in a **list** of strings representing the column names and pandas will return a dataframe containing only the values in those columns. The following code returns a dataframe containing the "Zinc_(mg)" and "Copper_(mg)" columns, in that order:
```
columns = ["Zinc_(mg)", "Copper_(mg)"]
zinc_copper = food_info[columns]

# Skipping the assignment.
zinc_copper = food_info[["Zinc_(mg)", "Copper_(mg)"]]
```
When selecting multiple columns, the order of the columns in the returned dataframe matches the order of the column names in the list of strings that you passed in. This allows you to easily explore specific columns that may not be positioned next to each other in the dataframe.

### Data Manipulation
The following code will divide each value in the "Iron_(mg)" column by 1000, and return a new Series object with those values:
```
div_1000 = food_info["Iron_(mg)"] / 1000
``` 
pandas allows us to use any of the arithmetic operators to scale the values in a numerical column:
```
# Adds 100 to each value in the column and returns a Series object.
add_100 = food_info["Iron_(mg)"] + 100

# Subtracts 100 from each value in the column and returns a Series object.
sub_100 = food_info["Iron_(mg)"] - 100

# Multiplies each value in the column by 2 and returns a Series object.
mult_2 = food_info["Iron_(mg)"]*2
```
In addition to transforming columns by numerical values, we can transform columns by other columns. When we use an arithmetic operator between two columns (Series objects), pandas will perform that computation in a pair-wise fashion, and return a new Series object. It applies the arithmetic operator to the first value in both columns, the second value in both columns, and so on.
```
water_energy = food_info["Water_(g)"] * food_info["Energ_Kcal"]
```
### Normalizing Columns
While there are many ways to normalize data, one of the simplest ways is called [rescaling](https://en.wikipedia.org/wiki/Feature_scaling#Rescaling). The outcome of rescaling is that every value in a numeric column will range between 0 and 1 (with the column's minimum value being 0 and the maximum value being 1). Here's the formula for rescaling:
![rescaling](images/rescaling.svg)