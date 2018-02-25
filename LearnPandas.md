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