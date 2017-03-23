## PySpark Intermediate Reference

### RDD Actions
#### Take Ordered
Internally sorts the RDD and takes the lowest (ascending) n elements

    top15 = some_RDD.takeOrdered(15)

2nd positional argument of `takeOrdered` used to specify a scoring function

    top15_kv_pair_values = some_RDD_kv_tuples.takeOrdered(15, lambda (k, v): -v)

### Access DB filesystem tools from spark notebook
    %fs

### MLLib
#### DenseVector
Use for efficient storage of vectors where there are lots of zeros

    from pyspark.mllib.linalg import DenseVector
