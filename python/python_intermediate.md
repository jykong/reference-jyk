### Intermediate Python Reference

#### Modules
    import package_name
    package_name.func()
    copy_var = package_name.var

#### Module Aliases
    import package_name as pack_alias
    pack_alias.func()
    copy_var = pack_alias.var

#### Classes
Defining a new class

    class SomeClass()
      def __init__(self):
        self.property_name = default_value

      def some_method(self):
        # do stuff with self.property_name
        return result

Creating an instance & using property / methods

    new_object = SomeClass()
    new_object.property_name
    new_object.some_method()

Constructer & method arguments

    class SomeClass()
      def __init__(self, arg):
        self.property_name = arg

    def some_method(self, arg):
      # do stuff with self & arg
      return result

    new_object = SomeClass(some_value)
    new_object.some_method(some_other_value)

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

#### List Comprehensions
Compact expression

    new_list = [some_func(elem) for elem in some_iterable]

Equivalent verbose expression in loop form

    new_list = []
    for elem in some_iterable:
      new_list.append(some_func(elem))

With a conditional

    new_list = [x for x in some_list if x == y]

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

#### Regular Expressions
    import re

    re.search("e_s", "some_string") != None           # evaluates to True
    re.sub("string", "replacement", "some_string")    # returns "some_replacement"
    re.sub("string", "replacement", "no_match")       # returns "no_match"
    re.findall("[str]", "some_string")                # returns ["s","s","t","r"]

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

#### Command Line / IDLE shell
Launch IDLE from terminal command line

    python

From IDLE:

    execfile('script.py')     # run a .py script in foreground

    import subprocess
    subprocess.call(['python', 'script.py'])          # Run program in background
    subprocess.check_output(['python', 'script.py'])  # Display the stdout

    exit()                    # close IDLE, return to command line
