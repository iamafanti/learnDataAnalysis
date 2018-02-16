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

