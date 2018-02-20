# learnDataAnalysis
This is the notebook for me to learn data science.
## 1. NumPy

### 1.1 Getting started with Numpy
The core structure of NumPy is <font color=#0099ff>ndarray</font> object, which stands for N-dimension array. A 1-dimensional array is often referred to as a vector while a 2-dimensional array is often referred to as a matrix. 
To use NumPy, we first need to import it into our python environment. NumPy is commonly imported using the alias **np**:

`import numpy as np`

We can construct ndarray object from python list using `np.array()` function. a. Vector `np.array([1,2,3])` b.Array `np.array([[53, 12, 15], [20, 21, 22], [31, 32, 33]])`

We can use ndarray's **shape** property to show the structure of an array. For example:

```
vector = numpy.array([1, 2, 3, 4])
print(vector.shape)
```

In the console, it will show a tuple of (4,) not an integer 4. 

```
matrix = numpy.array([[5, 10, 15], [20, 25, 30]])
print(matrix.shape)
```

In the console, it will show a tuple of (2,3) which means that the matrix has 2 rows and 3 columns. 

You may see that when making matrix using array(), the parameter is a list of lists. Each list item is a row of the matrix.

We can import dataset using [numpy.genfromtxt()](http://docs.scipy.org/doc/numpy-1.10.0/reference/generated/numpy.genfromtxt.html) function.
The name of the dataset is 'data.csv' and the data inside is seperated by commas which is called delimiter.
```
import numpy
data_set = numpy.genfromtxt("data.csv", delimiter=",")
```

The above code would read in a file named data.csv file into a NumPy array. NumPy arrays are represented using the numpy.ndarray class. What's more, a delimiter of the right kind must be chosen. If not, there may be some errors as the default parameter of delimiter in genfromtxt function is `None`.

Each value in a ndarray must have the same date type. [Ndarray's value types](http://docs.scipy.org/doc/numpy-1.10.1/user/basics.types.html) are similar to the types of Python such as bool, int, string, and float.
NumPy will automatically figure out an appropriate data type when reading in data or converting lists to arrays. You can check the data type of a NumPy array using the `dtype` property.

As I mentioned above, ndarray only have a data type. So `genfromtxt()` funciton can change the data to what it guesses is the best type. However, this can lead to some trouble. For example, when the function think float is the right type for the array, the strings will be changed to `nan` which means "not a number". NumPy assigns an `na` value, which stands for "not available", when the value doesn't exist. `nan` and `na` values are types of missing data. 

As NumPy displays numeric values in scientific notation by default, the number 1988 may be changed into 1.98800000e+03.

We can use `skip_header` parameter to specify how many lines of a dataset can be seen as headers. `dtype` parameter can limit genfromtxt function the data type it choose. For example, if set `dtype` to "U75", 1988 can be imported as "1988".

#### Slice of Numpy array
We can use the similar way to index arrays as python list. For example:
```
>> matrix = np.array([
                        [5, 10, 15], 
                        [20, 25, 30]
                     ])
>> matrix[1,2]
30
```
Like lists, vector slicing is from the first index up to but not including the second index. The first parameter in bracket is row number and the second one is column. 

The colon by itself : specifies that the entirety of a single dimension should be selected. Think of the colon as selecting from the first element in a dimension up to and including the last element. At the bottom are some typical examples:
```
>> matrix = np.array([
                    [5, 10, 15], 
                    [20, 25, 30],
                    [35, 40, 45]
                 ])
>> matrix[:,1]
array([10, 25, 40])
```

```
>> matrix = np.array([
                    [5, 10, 15], 
                    [20, 25, 30],
                    [35, 40, 45]
                 ])
>> matrix[:,0:2]
array([[ 5, 10],
       [20, 25],
       [35, 40]])
```
```
>> matrix[1:3,:]
array([[20, 25, 30],
       [35, 40, 45]])
```
```
>> matrix[1:3,1]
array([25, 40])
```
```
>> matrix = np.array([
                    [5, 10, 15], 
                    [20, 25, 30],
                    [35, 40, 45]
                 ])
>> matrix[1:3,0:2]
array([[20, 25],
       [35, 40]])
```

### 1.2 Compute with Numpy
An important feature of Numpy is that it can do comparisons for entire arrays and returns an array of boolean value. For example:
```
vector = numpy.array([5, 10, 15, 20])
vector == 10
```
The code above will generate the vector \[False, True, False, False\].
It is the same with matrix. For example:
```
matrix = numpy.array([
                    [5, 10, 15], 
                    [20, 25, 30],
                    [35, 40, 45]
                 ])
matrix == 25
```
The result is :
```
[
    [False, False, False], 
    [False, True,  False],
    [False, False, False]
]
```

The boolean matrix can be used to select intended data from an array as follows. 
```
vector = numpy.array([5, 10, 15, 20])  # crete an array
equal_to_ten = (vector == 10)   # create a boolean vector

print(vector[equal_to_ten])   #print out all the items fitted to boolean vector equal_to_ten
```
