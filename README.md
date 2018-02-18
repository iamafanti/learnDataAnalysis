# learnDataAnalysis
This is the notebook for me to learn data science.
## 1. NumPy
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

We can import dataset using [numpy.genfromtxt()](http://docs.scipy.org/doc/numpy-1.10.0/reference/generated/numpy.genfromtxt.html) function.
The name of the dataset is 'data.csv' and the data inside is seperated by commas which is called delimiter.
```
import numpy
data_set = numpy.genfromtxt("data.csv", delimiter=",")
```

The above code would read in a file named data.csv file into a NumPy array. NumPy arrays are represented using the numpy.ndarray class. What's more, a delimiter of the right kind must be chosen. If not, there may be some errors as the default parameter of delimiter in genfromtxt function is `None`.

Each value in a ndarray must have the same date type. [Ndarray's value types](http://docs.scipy.org/doc/numpy-1.10.1/user/basics.types.html) are similar to the types of Python such as bool, int, string, and float.
