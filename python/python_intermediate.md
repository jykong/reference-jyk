### Intermediate Python Reference

Show function documentation

    help(some_func)

Show available methods

    dir(some_object)

#### Modules
    import package_name
    package_name.func()
    copy_var = package_name.var

#### Module Aliases
    import package_name as pack_alias
    pack_alias.func()
    copy_var = pack_alias.var

#### Run from command line
    if __name__ == "__main__":
      # do stuff

    import sys
    if __name__ == "__main__":
      print(sys.argv[1])
      print(sys.environ["SOME_VARIABLE"])

#### Classes
Defining a new class

    class SomeClass():
      def __init__(self, arg):
        self.property1 = default_value
        self.property2 = arg

      def some_instance_method(self):
        # do stuff with self.property1 & self.property2
        return result

      @classMethod
      def some_class_method(self, arg):
        # do stuff
        return result

First argument of instance & class methods is always `self`

Creating an instance & using property / methods

    new_object = SomeClass(some_constructor_value)
    new_object.property_name
    new_object.some_instance_method()
    SomeClass.some_class_method(some_value)

#### Inheritance
All classes inherit the `object` class by default

    class SomeChildClass(ParentClass):
      ...

##### Function / Operator Overloading
Parent functions can be overloaded by having the child class define the function

Operators can be overloaded by defining their special function names

    __lt__(self, other):  # <
    __gt__(self, other):  # >
    __le__(self, other):  # <=
    __ge__(self, other):  # >=
    __eq__(self, other):  # ==
    __ne__(self, other):  # !=

#### Error Handling: Try/Except
    try:
      int('')       # statement produces an Error
    except:
      pass          # do this instead of stopping execution, pass -> do nothing

    try:
      int('')
    except Exception as exc:
      print(type(exc))
      print(str(exc))

#### Enumerate
    for i, item in enumerate(some_list, start=0):
      # do stuff, i will be integer index counter, defaults to count from 0

#### Dictionary Iteration, Items / Iteritems
Python 3

    for k,v in dict.items():
      # do stuff
Python 2

    for k,v in dict.iteritems():
      # do stuff

#### List Comprehensions
Compact expression

    new_list = [some_func(elem) for elem in some_iterable]

Equivalent verbose expression in loop form

    new_list = []
    for elem in some_iterable:
      new_list.append(some_func(elem))

With a conditional

    new_list = [x for x in some_list if x == y]

#### Map
    new_list = list(map(some_func, some_iterable))

`map` applies `some_func` to each element of `some_iterable` and then outputs the results via an iterable object

#### Filter
    new_list = list(map(some_boolean_func, some_iterable))

`filter` evaluates each element of `some_iterable` with `some_func` and outputs the elements that evaluate to `True` via an iterable object

#### Lambda Functions
One-time, anonymous functions

    lambda x,y: x+y

Equivalent to:

    def add_args(x,y):
      return x+y

#### Random Number Generation
    import random
    random.seed(seed_value)
    random.randint(x_min, x_max)
    random.random()       # returns random float between 0-1
    random.uniform(a,b)   # returns random float between a-b
    random.sample(sequence, n_samples)

    [random.randint(0,10) for _ in range(20)]   # list of 20 random ints between 0-10

#### Scoping & Inheritance
Functions create a local variable scope

    var = 0

    def func():
      var = 1
      return var == 1     # returns True

    var == 0              # evaluates to True

Globals can be accessed inside a local scope, but not written to

    global_var = 0

    def okay_func():
      return global_var + 1

    def bad_func():
      global_var += 1     # throws an UnboundLocalError

#### Overriding Built-in Functions
Built-in functions can be overwritten

    two = sum([1, 1])
    sum = 42
    sum([1, 1])   # throws Error

#### Argument Tuple
    arg_tuple = (some_argval1, some_argval2, some_argval3)
    some_3arg_func(*arg_tuple)

#### Argument Keyword Dictionary

    arg_dict = {'arg1': some_val1, 'arg2': some_val2}
    some_2arg_func(**arg_dict)

[Python args and kwargs example](http://www.saltycrane.com/blog/2008/01/how-to-use-args-and-kwargs-in-python/)

#### Regular Expressions
    import re

    re.search("e_s", "some_string") != None           # evaluates to True
    re.sub("string", "replacement", "some_string")    # returns "some_replacement"
    re.sub("string", "replacement", "no_match")       # returns "no_match"
    re.findall("[str]", "some_string")                # returns ["s","s","t","r"]

#### Measuring Performance Time
    import time
Use `perf_counter()` for user process + system time (incl. sleep). Use `process_time()` for user process time only. `clock()` is deprecated since 3.3.

    before = time.process_time()
    # some task
    after = time.process_time()

#### Timestamps
A Unix timestamp is a simple floating point value, with no explicit mention of day, month, or year. This floating point value represents the number of seconds that have passed since the epoch. The epoch is the first second of the year 1970. So, a timestamp of 0.0 would represent the epoch, and a timestamp of 60.0 would represent one minute after the epoch.

    import time
    current_unix_timestamp = time.time()

Use gmtime() to get a human-readable struct_time

    st = time.gmtime(unix_timestamp)
    st.tm_year
    st.tm_mon
    st.tm_mday
    st.tm_hour
    st.tm_min

Times calculated with the time module always follow UTC, or Coordinated Universal Time. This is the accepted time standard within the programming community. It corresponds to the mean solar time at 0° longitude, and does not follow daylight saving time. UTC corresponds roughly to Greenwich Mean Time, except that it does not follow daylight saving time.

#### Datetime
The datetime module has better support for working extensively with dates. With datetime, it is easier to work with different time zones and perform arithmetic (adding days, for example) on dates.

    import datetime
##### datetime class

    dt = datetime.datetime.now()
    dt = datetime.datetime.fromtimestamp(unix_timestamp)
    dt.year
    dt.month
    dt.day
    dt.hour
    dt.minute
    dt.second
    dt.microsecond

##### timedelta class

    td = datetime.timedelta(<args>)
Arguments for timedelta include

    weeks
    days
    hours
    minutes
    seconds
    milliseconds
    microseconds

##### Using datetime & timedelta objects

    today = datetime.datetime.now()
    diff = datetime.timedelta(days = 1)
    yesterday = today - diff
    tomorrow = today + diff

##### Formatting output
Format output string

    dt.strftime("%b %d, %Y")     #i.e. May 4, 2010
Parse input string

    dt = datetime.datetime.strptime("%b %d, %Y", "May 4, 2010")
[strftime & strptime documentation](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior)

#### Memory Inspection
Get variable's memory address

    id(some_var)
Get variable's memory size (in bytes)

    import sys
    sys.getsizeof(some_var)

#### Base Conversion
##### Ordinals
    ascii_integer_value = ord('c')
    unicode_integer_value_256 = ord("\u0100")   # unicode is encoded in hex

##### Hex Values
    some_hex_str = "FF"
    hex_str_value = hex(some_int)
    base10_value255 = int(some_hex_str, 16)

##### Binary Values
    some_binary_string = "10001"
    bin_str_value = bin(some_int)
    base10_value257 = int(some_binary_string, 2)

#### Counter object
Use the Counter object to obtain sorted frequency counts

    from collections import Counter

    counter_object = Counter(some_list)
    top5_most_common_items = counter_object.most_common(5)

#### Command Line / IDLE shell
Launch IDLE from terminal command line

    python

From IDLE:

    execfile('script.py')     # run a .py script in foreground

    import subprocess
    subprocess.call(['python', 'script.py'])          # Run program in background
    subprocess.check_output(['python', 'script.py'])  # Display the stdout

    exit()                    # close IDLE, return to command line

#### Parallel Processing / Multithreading
    import threading

    some_thread = threading.Thread(target=some_func, args=[arg1, arg2])
    some_thread.start()
    # do other stuff
    some_thread.join()    # wait for thread to finish

Mutual Exclusion
    lock = threading.Lock()
    lock.acquire()
    # critical region
    lock.release()

#### Generators
Generators are lazy evaluated one-time iterators. Any function definition using `yield` produces a generator definition instead of a normal function definition.

    def like_range(n):
      i = 0
      while i != n:
        yield i
        i += 1

    for x in like_range(10000):
      # do stuff

`like_range` performs like the built-in `range` generator. In this case, it does not create a list of 10000 values in memory. Instead, each successive value is generated as the generator function is triggered each time the `for` loop is executed.
