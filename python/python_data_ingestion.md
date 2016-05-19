## Python Data Ingestion
CSV, APIs, JSON, and Web Scraping

### CSV
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

### APIs
    import requests

#### Basic GET call
    url = "http://somewebsite.com/data.json"      # always use double quotes for urls
    response = requests.get(url)
    status_code = response.status_code
    headers = response.headers                    # returns a dictionary

#### Passing in Parameters
Use a dictionary to pass in parameters

    dict = {"var1":some_val1, "var2":some_val2}
    response = requests.get(url, params=dict)

Equivalent hardcoded URL string

    # some_val1 = 55, some_val2 = 66
    url = "http://somewebsite.com/data.json?var1=55&var2=66"
    response = requests.get(url)

#### Passing in a Header
Use a dictionary to pass in a header

    header = {"var1":some_val1}
    response = request.get(url, headers=header)

#### Basic POST / PUT / PATCH calls
    response = requests.post(url, json=payload_dict)
    response = requests.put(url, json=payload_dict)
    response = requests.patch(url, json=payload_dict)
    status_code = response.status_code

### JSON
    import json

#### Loads & Dumps
Loads: JSON string to data structures (lists & dicts)

    data = json.loads(json_string)

Dumps: Data structures (lists & dicts) to JSON string

    data1 = some_list
    data2 = some_dict
    json_string1 = json.dumps(data1)
    json_string2 = json.dumps(data2)

#### Get json data from request
    url = "http://somewebsite.com/data.json"
    response = requests.get(url)
    data = response.json()    # returns data a data structure

### Web Scraping w/ BeautifulSoup
    from bs4 import BeautifulSoup
    response = requests.get(url)
    content = response.content
    parser = BeautifulSoup(content, 'html.parser')

#### Dot notation
Use . to access individual child elements within the DOM

    body = parser.body
    title_text = parser.head.title.text

#### find_all
Use find_all to return a list of child & sub-child (recursive) tags

    title_text = parser.find_all("head")[0].find_all("title")[0].text
    all_p_list = parser.find_all("p")
    specific_p = parser.find_all("p", class_="specific", id="the_one")[0]

#### select
Use select to return a list of elements via CSS notation

    elem_list_by_class = parser.select(".class_name")
    elem_list_by_id = parser.select("#id_name")
    nested_elems = parser.select("body div .class_name #id_name")
