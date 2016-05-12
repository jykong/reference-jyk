#### Handling CSV, APIs, JSON

#### Python CSV library
    import csv
    import unicodecsv   # same as csv modeule, but with unicode support

See also basic_pandas_reference.md for info on pandas.read_csv()

#### CSV reader
    with open("file.csv","r") as f:
      reader = csv.reader(f)    # read in as a string
      data = list(reader)       # convert to a list of lists

#### CSV dictreader
Read in CSV as a dictionary, first row treated as header / keys
    with open("file.csv","rb") as f:
      reader = unicodecsv.dictreader(f)

    for row in reader:
      # do stuff
