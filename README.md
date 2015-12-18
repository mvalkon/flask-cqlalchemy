# Flask-CQLAlchemy

[![Latest Version](https://img.shields.io/pypi/v/flask-cqlalchemy.svg)](https://pypi.python.org/pypi/Flask-CQLAlchemy)
[![Build Status](https://travis-ci.org/thegeorgeous/flask-cqlalchemy.svg?branch=master)](https://travis-ci.org/thegeorgeous/flask-cqlalchemy)
[![Code Climate](https://codeclimate.com/github/thegeorgeous/flask-cqlalchemy/badges/gpa.svg)](https://codeclimate.com/github/thegeorgeous/flask-cqlalchemy)
[![Downloads](https://img.shields.io/pypi/dm/flask-cqlalchemy.svg)](https://pypi.python.org/pypi/Flask-CQLAlchemy)


Flask-CQLAlchemy handles connections to Cassandra clusters
and gives a unified easier way to declare models and their
columns

## Installation
```
pip install flask-cqlalchemy
```

## Example
```
#example_app.py
import uuid
from flask import Flask
from flask.ext.cqlalchemy import CQLAlchemy

app = Flask(__name__)
app.config['CASSANDRA_HOSTS'] = ['127.0.0.1']
app.config['CASSANDRA_KEYSPACE'] = "cqlengine"
db = CQLAlchemy(app)


class User(db.Model):
    uid = db.columns.UUID(primary_key=True, default=uuid.uuid4)
    username = db.columns.Text(required=False)
```

## Usage
Start a python shell
```
>>from example_app import db, User
>>db.sync_db()
>>user1 = User.create(username='John Doe')
```
For a complete list of available method refer to the cqlengine [Model documentation](http://datastax.github.io/python-driver/api/cassandra/cqlengine/models.html)

## Configuration Options
CQLAlchemy provides all the option available in the cqlengine connection.setup() method

* CASSANDRA_HOSTS - A list of hosts
* CASSANDRA_KEYSPACE - The default keyspace to use
* CASSANDRA_CONSISTENCY - The global default ConsistencyLevel
* CASSANDRA_LAZY_CONNECT - True if should not connect until first use
* CASSANDRA_RETRY_CONNECT - True if we should retry to connect even if there was a connection failure initially
* CASSANDRA_SETUP_KWARGS - Pass-through keyword arguments for Cluster()

## Tutorial
For a tutorial on how to use Flask-CQLAlchemy check this [post](http://thegeorgeous.com/2015/06/17/creating-a-tumblelog-with-flask-and-flask-cqlalchemy-I.html)
