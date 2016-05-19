### Basic Python Reference

#### Basic Built-in Functions
    print('something')
    type(var)   # returns data type
    len(obj)    # returns length
    sorted(some_list)    # returns a sorted some_list

#### Strings
    str = 'this is a string'
    str = "this is also a string"   # safer to use
    url = "http://doublesquotesfor.urls"
    # use double quotes for URLs -- I don't know why

#### Int / Float
    x = 1         # integer
    y = 1.0       # float
    x = int(y)    # cast to int
    y = float(x)  # cast to float

#### Booleans
    bool_true = True
    bool_false = False

#### Null Reference Keyword: None
    null_reference = None

#### Comparison / Boolean Operators
All comparison and boolean operators return a boolean value

    a == b
    a != b

    a > b
    a >= b
    a < b
    a <= b

    a and b
    a or b
    a ^ b     # XOR

#### Arithmetic Operators
    a + b
    a - b
    a * b
    a / b
    a // b    # floor division
    a ** b    # power / exponent
Reassignment versions

    a += b
    a -= b
    a *= b
    a /= b
    a //= b
    a **= b

#### If statements
    if expression:
      # do this if variable 'expression' evaluates to True
    else:
      # do this if variable 'expression' evaluates to False

#### Lists
    new_list = []               # declare new_list as empty list
    new_list = [1, 'str', 0.7]  # declare new_list with values
    new_list[0]                 # first element
    new_list[-1]                # last element
    new_list[0:5]               # list of first five elements
    new_list.append('item')     # add to the end of the list

#### Sets
Similar to lists, except all unique / no duplicate values, and unordered

    new_set = set()
    new_set.add("item")
    new_set.remove("item")

#### Tuples
Similar to lists, except immutable (ordered)

    new_tuple = ()
    new_tuple = (10,11,12)
    ten = new_tuple[0]

#### Dictionaries
    empty_dict = {}
    dict = {
      "init_key1": init_val1,
      "init_key2": init_val2
    }
    dict["some_key"] = some_value   # Add or modify

#### In statments
    bool_result = item in some_list
    # search some_list for object item, returns True if found

    bool_result = key in dict
    # searches keys of dict, returns True if found

#### Functions
    def basic_func(arg1, arg2):
      # do stuff
      return result

    def some_func(required_arg1, optional_arg="default_value"):
      if optional_arg:
        # do stuff
      return result

    called_func(positional_arg1, positional_arg2, optional_arg1=some_val, optional_arg2=some_val)

    def multi_return_func(arg1)
      # do stuff
      return r1, r2

    out1, out2 = multi_return_func(some_val)

#### File
    f = open('/filepath', 'r')    # open file, read access
    f = open('/filepath', 'rwb')  # read & write as binary
    f.close()                     # close file

    with open('/filepath', 'r') as f:
      # do stuff, file closes outside of scope
      # effectively the same as above

    str = f.read()                # read in file as a string

#### Loops
    for each_element in some_list:
      # do stuff with variable: each_element
      # iterates over some_list, actually some Iterable

    for i in range(0,10):
      # do stuff, 10 times
      # simple counter based loop

    for i in range(10):
      # same as above, one argument range assumes initial value of 0

    for i in range(0, 20, 2)
      # step size of 2

    for i in xrange(0,10):
      # only for Python 2 !!!, Python 3 just uses range()
      # functionally same as using range, except doesn't create a list
      # more efficient

    for k, v in some_dict.items():
      # .items() outputs the dictionary as a list of tuple pairs
      # using items() iterates over keys and values simultaneously
      # easier to use v instead some_dict[k] repeatedly

    list_of_tuples = [(1,2,3),(100,200,300),(0,1,1)]
    for x,y,z in list_of_tuples:
      # do stuff with x,y,z
