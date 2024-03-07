---
toc: True
comments: True
layout: post
title: Flask Server
description: Flask server setup.
type: hacks
courses: {'csp': {'week': 4, 'categories': ['4.A']}}
categories: ['C1.4']
---

```python
%%python --bg

from flask import Flask, jsonify
from flask_cors import CORS

# initialize a flask application (app)
app = Flask(__name__)
CORS(app, supports_credentials=True, origins='*')  # Allow all origins (*)

# ... your existing Flask

# add an api endpoint to flask app
@app.route('/api/data')
def get_data():
    # start a list, to be used like a information database
    InfoDb = []

    # add a row to list, an Info record
    InfoDb.append({
        "FirstName": "John",
        "LastName": "Mortensen",
        "DOB": "October 21",
        "Residence": "San Diego",
        "Email": "jmortensen@powayusd.com",
        "Owns_Cars": ["2015-Fusion", "2011-Ranger", "2003-Excursion", "1997-F350", "1969-Cadillac"]
    })

    # add a row to list, an Info record
    InfoDb.append({
        "FirstName": "Shane",
        "LastName": "Lopez",
        "DOB": "February 27",
        "Residence": "San Diego",
        "Email": "slopez@powayusd.com",
        "Owns_Cars": ["2021-Insight"]
    })
    
    return jsonify(InfoDb)

# add an HTML endpoint to flask app
@app.route('/')
def say_hello():
    html_content = """
    <html>
    <head>
        <title>Hellox</title>
    </head>
    <body>
        <h2>Hello, World!</h2>
    </body>
    </html>
    """
    return html_content

if __name__ == '__main__':
    # starts flask server on default port, http://127.0.0.1:5001
    app.run(port=5001)

```


```python
%%script bash

# After app.run(), see the the Python process
lsof -i :5001

```

    COMMAND     PID    USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
    python3.9 21824 remyliu    4u  IPv4 0x3c93380141362051      0t0  TCP localhost:commplex-link (LISTEN)



```python
import requests
res = requests.get('http://127.0.0.1:5001/api/data')
res.json()
```




    [{'DOB': 'October 21',
      'Email': 'jmortensen@powayusd.com',
      'FirstName': 'John',
      'LastName': 'Mortensen',
      'Owns_Cars': ['2015-Fusion',
       '2011-Ranger',
       '2003-Excursion',
       '1997-F350',
       '1969-Cadillac'],
      'Residence': 'San Diego'},
     {'DOB': 'February 27',
      'Email': 'slopez@powayusd.com',
      'FirstName': 'Shane',
      'LastName': 'Lopez',
      'Owns_Cars': ['2021-Insight'],
      'Residence': 'San Diego'}]




```python
%%script bash

lsof -i :5001 | awk '/Python/ {print $2}' | xargs kill -9

```
