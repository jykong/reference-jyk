## Spark Python API Reference

    from pyspark import SparkContext
    sc = SparkContext("local", "App Name")

#### Resilient Distributed Database (RDD)
Data is stored as immutable RDDs. They are immutable (cannot be overwritten) for performance reasons. Bits and parts of RDDs can be anywhere in the data cluster.

#### Lazy Evaluation
A lot of commands in Spark are done via lazy evaluation. Instead of executing the command immediately, the command is set up and promised for when it is needed. An analogy would be setting up an on-demand assembly line that is only triggered to operate when a product is needed at the end, as opposed to operating every step every time regardless to whether or not the next step needs it.

The Catalyst Optimizer is the engine that schedules evaluation for Spark SQL. [Read more here](https://databricks.com/blog/2015/04/13/deep-dive-into-spark-sqls-catalyst-optimizer.html)

#### Driver vs Executors
The Driver is the program running on your computer

Executors are workers performing operations on nodes

#### Basics
    new_rdd = sc.parallelize(range(10))

`new_rdd` is now an RDD. `parallelize()` is lazy evaluated.

    new_rdd.take(5)      # returns & prints the first 5 elements

`take` is an action. This causes `parallelize()` to evaluate, at least for the first 5 elements.

##### Inspection
Display the number of partitions the data is split over

    new_rdd.getNumPartitions()

### RDD Transformations
Transformations are lazy evaluated. Transformations are performed by the executors.

##### Parallelize
Import python iterable into an RDD

    new_rdd = sc.parallelize(some_list, numSlices)

2nd positional argument of `parallelize()` specifies the number of slices to divide the RDD into. Slices can be automatically spread across nodes and increase parallelism.

##### Map
Operates much like Python map

    new_rdd = some_rdd.map(some_func)

Map return values have a 1-to-1 mapping with the input data.

Use `.flatMap()` to combine output into one single flat list, instead of nested lists. Flat map is okay with functions that do not return values for every input data.

    new_rdd = some_rdd.flatMap(some_func)

##### Sample


##### Filter
Operates much like Python filter

    new_rdd = some_rdd.filter(some_boolean_func)

##### Reduce By Key
Does an grouped reduction / aggregation on an array of 2-element tuples. First item in the tuples is the key, the second item is reduced / aggregated by the specified function.

    reduced_rdd = some_rdd_of_tuples.reduceByKey(lambda x,y: some_func(x,y))

#### Sort By
rdd.sortBy(value_f, False)

### RDD Actions
Actions involve the driver & executors.
#### Take
Similar to `head()` in Pandas. Returns top n elements. Returns as a list of Row objects.

    some_rdd.take(n_elements)

#### Count
Similar to `len()`

    some_rdd.count()

#### Cache
`cache()` is used to tell Spark to persist an RDD (keep it in memory). This can be used to avoid unnecessary re-computation in subsequent actions.

    some_rdd.cache()

`unpersist()` is used to tell Spark to remove an RDD from memory. This is used to free up memory to prevent Spark from evicting other useful RDDs automatically.

    some_rdd.unpersist()

`is_cached` is a boolean property that can be checked to see if an RDD is cached

    some_rdd.is_cached

#### Broadcast
`broadcast()` sends an RDD to each partition. Use to optimize performance for frequently referenced data

#### Collect
Returns all the rows. **WARNING: *Use carefully with large datasets***

    some_rdd.collect()

#### Count By Key
Combines reduceByKey() & count(). Ends with collect()
    some_rdd.countByKey()

### Running a Spark Application
    from pyspark import SparkConf, SparkContext
    conf = SparkConf().setAppName("MyApp")
    sc = SparkContext(conf=conf)

To shut down Spark:

    sc.stop() or sys.exit(0)

#### Use spark-submit
    spark-submit sparkapp.py args

### Web UI
    localhost:4040/jobs
