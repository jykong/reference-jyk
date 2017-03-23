### Basic Numpy Reference

[Numpy Reference Documentation](http://docs.scipy.org/doc/numpy/reference/)

#### Import Numpy
    import numpy
Frequently imported as `np`

    import numpy as np
#### Initializing Arrays
    vector = np.array([1,2,3,4])
    matrix = np.array([[1,2],[3,4]])
    matrix = np.empty(shape=(100,100))

    1d_row_matrix = np.array([[1,2,3,4]])   # extra [] makes it (4,1) instead of (4,)
    1d_col_matrix = np.array([[1],[2],[3],[4]])

Linear values

    vector = np.linspace(x_min, x_max, n_samples)
    vector = np.arange(x_min, x_max, x_step_size)

#### Shape Property
Outputs dimensions of the array as a tuple

    tuple_result = vector.shape     # (x,)
    tuple_result = matrix.shape     # (x_rows, y_columns)

#### Reshape
    1d_col_matrix = vector.reshape(-1,1)

#### Transpose
    1d_col_matrix = vector.T

#### Data Type Property
Every element of a NumPy array must have the same data type

    type_result = vector.dtype

#### Reading In Data
    np.genfromtext("file.csv", delimiter=",")
    np.genfromtext("file.csv", dtype="U75", delimiter=",", skip_header=True)

#### Indexing Arrays
    idx_val = vector[i]
    mat_val = matrix[i,j]

#### Slicing Arrays
    vector = np.array([0,1,2,3,4])
    sliced_vector = vector[0:3]   # returns [0,1,2]
    col0 = matrix[:,0]            # returns all rows, 0th column
    row0 = matrix[0,:]            # returns all columns, 0th row

#### Array Comparisons
Compares each element of array against a single value
Outputs a Boolean array (mask) with results

    bool_mat = (matrix[a:b,x:y] == some_value)
    bool_mat = np.arrray([[True, False]
                [False, True]])  # example output

#### Selection / Masking
Boolean arrays (masks) can be used in the index operator to select True elements and omit False elements

    vector = np.array([0,1,2,3,4])
    bool_vector = np.array([True, False, True, False, False])
    new_vector = vector[bool_vector]
    new_vector = np.array([0,2])   # example output

#### Replace values
    vector = np.array([0,1,2,3,4])
    vector = 5
    vector = np.array([5,5,5,5,5])   # example output

#### Casting Data Types
    vector_as_float = vector.astype(float)

#### Joining NumPy Arrays
`hstack()`: horizontal concatenation

    vector1 = np.array([1,2])
    vector2 = np.array([3,4])
    result = np.hstack((vector1, vector2))
    result = np.array([1,2,3,4])

`vstack()`: vertical concatenation

    vector1 = np.array([1,2])
    vector2 = np.array([3,4])
    result = np.hstack((vector1, vector2))
    result = [[1,2],[3,4]]

`column_stack()`: Pandas-like column appending

    matrix = np.array([[0,1],[1,0]])
    vector = np.array([2,3])
    result = np.column_stack(matrix, vector)
    result = np.array([[0,1,2],[1,0,3]])

#### Basic Statistics
    vector.sum()
    vector.mean()
    vector.median()
    vector.min()
    vector.max()
    vector.argmin()   # returns array of indices of min values
    vector.argmax()   # returns array of indices of max values

    matrix.sum()        # defaults to row-wise
    matrix.sum(axis=0)  # column-wise

#### More Statistics
[NumPy Stats Routines](http://docs.scipy.org/doc/numpy/reference/routines.statistics.html)

    np.<routine>()

    covariance = np.cov(x_vector, y_vector)[0,1]

#### Randomization
Generate random integers

    vector = np.random.randint(x_min, x_max, n_samples)

Generate random floats from 0.0 to (but not including) 1.0

    vector = np.random.random(n_samples)
    vector = np.random.sample(n_samples)
    vector = np.random.ranf(n_samples)
    vector = np.random.random_sample(n_samples)

Randomly choose from an array-like

    vector = np.random.choice(some_array_like, n_samples)

Random permutation

    vector = np.random.permutation(some_array_like)

[See docs for non-uniform distributions](http://docs.scipy.org/doc/numpy-1.10.1/reference/routines.random.html#distributions)

#### Output to list
    vector_list = vector.tolist()
    nested_lists = matrix.tolist()

#### Linear Algebra
##### Inverse
Matrix * Inverse = Identity Matrix

    inverse_matrix = np.linalg.inv(matrix)
