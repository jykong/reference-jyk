## Basic Pandas Reference
Pandas is built on top of Numpy. Uses DataFrames and Series instead of Arrays for easier manipulation of data.

#### Importing Pandas
    import pandas
Frequently imported as `pd`

    import pandas as pd

#### Reading CSV
Reads in CSV as a DataFrame, automatically treating 1st row as header

    dataframe = pandas.read_csv("file.csv")

In case of encoding error, trying a different encoding

    dataframe = pandas.read_csv("file.csv", encoding="iso-8859-1")

[](https://docs.python.org/3/library/codecs.html#standard-encodings)

#### Inspecting Dataframes
    dataframe.head(5))    # outputs the first 5 rows
    dataframe.shape       # outputs the dimensions as a tuple
    dataframe.columns     # outputs the column headers as an index
    dataframe.index       # outputs the row index
    dataframe.values      # outputs values as a list

#### Empty Values: NaN
Empty / null values in a DataFrame or Series are represented with NaN (Not a Number)

### Series
#### Series data object
Instead of returning 1-D arrays as vectors like NumPy, Pandas returns a Series object.

    series_object = dataframe["col_name"]
    series_object = dataframe.loc[0]

When outputting a column from a DataFrame, the row index becomes the Series index.

When outputting a row from a DataFrame, the column header becomes the Series index.

Each Series object has an index AND a integer position. The index can handle a variety of datatypes. Each entry in the index is mapped to a corresponding value, similar to a dictionary.

    mapped_value = series_object["some_index_element"]

Series objects can also be addressed by position.

    value = series_object[0]
    sublist = series_object[2:5]

Creating a Series object via Series constructor

    from pandas import Series
    series_object = Series(index=array-like1, data=array-like2)
    # len(array-like1) must be equal to len(array-like2)

#### Manipulating Series

Converting Series object to dictionary, index -> keys

    dict = series_object.to_dict()

Outputting the index / values

    index = series_object.tolist()
    values = series_object.values

Reindexing

    reindexed_series = series_object.reindex(new_index)

Sorting

    index_sorted = series_object.sort_index()
    values_sorted = series_object.sort_values()

Arithmetic operations on Series values are treated like NumPy arrays

    scaled_seies_vector = series_object/100
    pairwise_sum_series = series1 + series2

Comparison operations on Series values output Boolean Series like NumPy

    bool_series = (series_object == "magic string")

Boolean Series can be used to select / deselect items in a Series (masking)

    subsetted_series = series_object[bool_series]
    subsetted_series = series_object[series_object < 100]

#### Checking for NaN values
    boolean_series = pandas.isnull(some_series_object)    # Series values True if null

### DataFrames
Like Series objects, dataframe rows can be accessed either by position or index

#### Selecting Dataframe Rows by Position / Index
dataframe.iloc[] - get [row,col] by position, sorting / dropping rows may change position of rows relative to their index

    dataframe.iloc[0]        # outputs the first row as a Series
    dataframe.iloc[0:3]      # slice 0-2 rows of dataframe
    dataframe.iloc[[0,1,2]]  # same as above, except enumerating rows with a list

    dataframe.iloc[0,0]      # outputs the first row element of the first column
    dataframe.iloc[:,0]      # outputs the first column

dataframe.loc[] - get [row,col] by index

    dataframe.loc["row_index", "col_index"]

[](http://pandas.pydata.org/pandas-docs/stable/indexing.html)

[](http://pandas.pydata.org/pandas-docs/stable/cookbook.html#cookbook-selection)

#### Alternative Selecting Dataframe Columns by Index
    dataframe["col_name"]         # outputs the column matching "col_name"
    dataframe[["col1", "col2"]]   # outputs multiple columns

#### Adding / Modifying Dataframe Columns
    dataframe["new_col_name"] = some_series_object
    dataframe["existing_col_name"] = some_series_object

#### ***WARNING*** about chained indexing
    dataframe["col1"]["col2"] = something   # will throw an warning

    new_df = dataframe["col1"]
    new_df["col2"] = something              # equivalent, will also throw a warning

First, `dateframe["col1"]` initiates a `__getitem__` call that may return a copy of dataframe. Then, `new_df["col2"]` initiates a `__setitem__` call that will try write on what may be a copy, which would not update the original dataframe.

[](http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy)

See section on "Setting With Copy" [](http://tomaugspurger.github.io/modern-1.html)

#### Force Copy
    new_df = pandas.DataFrame(dataframe)    # call constructor

#### Dropping Rows / Columns
    new_df = dataframe.drop('row_index')                            # drop row by index
    dataframe.drop('col_name', axis=1, inplace=True)                # drop col by name
    new_df = dataframe[dataframe['col_name'] != 'unwanted_value']   # drop row by value

#### Apply
    series_result = dataframe.apply(single_arg_func)          # calls on each column
    series_result = dataframe.apply(single_arg_func, axis=1)  # calls on each row

    def single_arg_func(some_series):           # example single argument function
      # do stuff with series
      return series_object

    df_result = dataframe.apply(lambda x: x*2)            # doubles each element
    series_result = dataframe.apply(lambda x: np.sum(x))  # sums across rows

#### Sorting Dataframes
Sort defaults to outputig a new dataframe. Use inplace to modify existing dataframe.

    dataframe.sort("col_to_sort_by", inplace=True, ascending=False)

#### Custom Index
Drop current index and use a specified column as the index instead.

    reindexed_df = dataframe.set_index("col_name", inplace=False, drop=True)

#### Data Types
    dataframe.dtypes

    * object (String)
    * int
    * float
    * datetime
    * bool

#### Handling NaN values
dataframe.dropna()

    new_dataframe = dataframe.dropna()        # Drop all rows with NaN values
    new_dataframe = dataframe.dropna(axis=1)  # Drop all columns with NaN values
    new_dataframe = dataframe.dropna(subset=["col1", "col2"])   # Drop all rows with NaN in col1 and col2

#### Other Useful Functions

dataframe.reset_index()

    reindexed_df = dataframe.reset_index(drop=True)        # Resets index based on current positions
    dataframe.reset_index(drop=True, inplace=True)         # Inplace version

dataframe.mean()

    scalar_val = dataframe["col"].mean()    # Calculates mean, automatically omits NaN values
