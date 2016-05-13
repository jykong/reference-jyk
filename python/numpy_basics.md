### Basic Numpy Reference

[Numpy Reference Documentation](http://docs.scipy.org/doc/numpy/reference/)

#### Import Numpy
    import numpy
Frequently imported as `np`

    import numpy as np
#### Initializing Arrays
    vector = numpy.array([1,2,3,4])
    matrix = numpy.array([[1,2],[3,4]])

    vector = numpy.arange(x_min, x_max, x_interval)   # Array Range

#### Shape Property
Outputs dimensions of the array as a tuple

    tuple_result = vector.shape
    tuple_result = matrix.Shape

#### Data Type Property
Every element of a Numpy array must have the same data type

    type_result = vector.dtype

#### Reading In data
    numpy.genfromtext("file.csv", delimiter=",")
    numpy.genfromtext("file.csv", dtype="U75", delimiter=",", skip_header=True)

#### Indexing Arrays
    idx_val = vector[i]
    mat_val = matrix[i,j]

#### Slicing Arrays
    vector = numpy.array([0,1,2,3,4])
    sliced_vector = vector[0:3]   # returns [0,1,2]
    col0 = matrix[:,0]            # returns all rows, 0th column
    row0 = matrix[0,:]            # returns all columns, 0th row

#### Array Comparisons
Compares each element of array against a single value
Outputs a Boolean array (mask) with results

    bool_mat = (matrix[a:b,x:y] == some_value)
    bool_mat = numpy.arrray([[True, False]
                [False, True]])  # example output

#### Selection / Masking
Boolean arrays (masks) can be used in the index operator to select True elements and omit False elements

    vector = numpy.array([0,1,2,3,4])
    bool_vector = numpy.array([True, False, True, False, False])
    new_vector = vector[bool_vector]
    new_vector = numpy.array([0,2])   # example output

#### Replace values
    vector = numpy.array([0,1,2,3,4])
    vector = 5
    vector = numpy.array([5,5,5,5,5])   # example output

#### Casting Data Types
    vector_as_float = vector.astype(float)

#### Basic Statistics
    vector.sum()
    vector.mean()
    vector.median()
    vector.min()
    vector.max()
    vector.argmin()   # returns array of indices of min values
    vector.argmax()   # returns array of indices of max values

#### More Statistics
[NumPy Stats Routines](http://docs.scipy.org/doc/numpy/reference/routines.statistics.html)

    numpy.<routine>()

    covariance = numpy.cov(x_vector, y_vector)[0,1]
