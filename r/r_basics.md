## R Basics Reference

### Basics
* Assignment: `x <- 10`
* Print: `print(x)`
* Data Type: `class(x)`
* Strings: `"some_string"`
* Help: `help(some_function)`

### Vectors
    vector <- c(0,1,2)

Vectors can only be of a single data type. If a string is mixed in with a numeric vector, the numbers will be cast as strings.

### Comparison
    identical(x,y)  # returns boolean TRUE or FALSE

### Addressing
    vector[1]   # gets first element of the collection

### Length
    vectorLength = length(vector)

### Arithmetic / Comparison Operations
Scalar operations are performed on every element of a vector

Vector operations is performed element-wise. If the vectors aren't the same length, the values from the shorter vector are repeatedly recycled.

Comparison operators return a boolean value (TRUE or FALSE)

### Masking
Boolean vectors can used to select individual elements of another vector

    filtered_vector = some_vector[boolean_mask_vector,]

### Matrices
    newMatrix <- matrix(someVector, nRows, nCols)

    first_row_second_column <- newMatrix[1,2]
    first_row <- newMatrix[1,]
    second_column <- newMatrix[,2]

Matrices can only be of a single data type.

### Data Frames
    new_df <- data.frame(vector1, vector2)

Columns addressable by column names

    col1_dataframe <- dataframe["col1"]
    col1_vector <- dataframe[,"col1"]
    col1_vector <- dataframe$col1
    col1_elem1 <- dataframe[1, "col1"]

    number_of_rows <- nrow(dataframe)
    first_five <- head(dataframe, 5)
    last_five <- tail(dataframe, 5)

    print(str(dataframe))   # str outputs human readable info on any R object

[Extract or Replace Parts of a Data Frame](https://stat.ethz.ch/R-manual/R-devel/library/base/html/Extract.data.frame.html)

### Import CSV data
    dataframe <- read.csv("filename.csv")

### Aggregation Functions
    sum()
    max()
    min()
    which.max()   # index of max value
    which.min()   # index of min value

### Value Counts / Table
    print(table(vector))

### User-defined Functions
    some_func <- function(x, y) {
      return(x + y)
    }
    five <- some_func(2, 3)

### String Manipulation
#### Substring
    a_few <- substr("some_string", 1, 4)  # returns "some"
    strings = c("prefix", "preview", "pre-conceived")
    three_pre <- substr(strings, 1, 3)    # substring applied to each element

### Casting
    as.character()

### Datetime
    as.Date("06/01/2016", "%m/%d/%Y")

### Null Values
`NA` is the null value for missing data

    cleaned_data = na.omit(data)
