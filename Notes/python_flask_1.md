# Python Flask 

## Table of Contents
1) [Introduction](#id1)
2) [Styling & Templates](#id2)
3) [Sending data to templates](#id3)
4) [Template Inheritance](#id4)
5) [Models & Databases](#id5)
6) [Project Restructure](#id6)
7) [Model Relationships](#id7)
8) [Flask Forms](#id8)
9) [Flask Validations](#id9)
10) [Flash messages & Advanced Validations](#id10)
11) [User Authentication](#id11)

***

<div id="id1"></div>

### 1) Introduction


>  pip install flask

> check using `flask --version`
>```
>Python 3.10.1
>Flask 2.1.3
>Werkzeug 2.2.0
>```

NOTE: `print(__name__)` prints `__main__` in python

***

#### Hello world in flask

```python
from flask import Flask
app = Flask(__name__)


@app.route("/")   # Decorator
def hello_world():
    return "Hello World!!!"
```

> Open terminal and set environment variable to this file name `set FLASK_APP=market.py`
> 
> `flask run`
> 
>```
> * Serving Flask app 'market.py' (lazy loading)
> * Environment: production
>   WARNING: This is a development server. Do not use it in a production deployment.
>   Use a production WSGI server instead.
> * Debug mode: off
> * Running on http://127.0.0.1:5000 (Press CTRL+C to quit)
>
>```


Now edit the return statement to `return "<h1>BIGGER Hello World!!!</h1>"`

This will print the text bigger. But each time when we modify code, we need to restart flask server. To avoid that turn on the debug mode

`set FLASK_DEBUG=1`

Turn this off before deploying in production
***

#### Creating another route (new page)

```python
@app.route("/about")
def about_page():
    return "<h1>About Page</h1>"
```

`http://127.0.0.1:5000/about` --> this will show About Page

***

#### Dynamic route

```python
@app.route("/about/<username>")
def about_page(username):
    return f"<h1>About Page of { username }</h1>"
```
* here `f` indicates it is a formatted string
* `http://127.0.0.1:5000/about/Sam` --> displays `About Page of Sam` text in web

***
***

<div id="id2"></div>

### 2) Styling & Templates 

#### Templates folder

* Create `templates` folder inside project (say here 'flaskMarket')
* place html files in it (say `home.html`)
* Go to bootstrap framework docs and get starter template html code and paste it in this html file - `https://getbootstrap.com/docs/4.5/getting-started/introduction/`

* Use below code
    ```python
    from flask import Flask, render_template
    app = Flask(__name__)
    
    
    @app.route("/")   # Decorator
    def hello_world():
        return render_template("home.html")
    ```

* `home.html` code from bootstrap site

    ```html
    <!doctype html>
    <html lang="en">
      <head>
        <!-- Required meta tags -->
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    
        <!-- Bootstrap CSS -->
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css" integrity="sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2" crossorigin="anonymous">
    
        <title>Hello, world!</title>
      </head>
      <body>
        <h1>Hello, world!</h1>
    
        <!-- Optional JavaScript; choose one of the two! -->
    
        <!-- Option 1: jQuery and Bootstrap Bundle (includes Popper) -->
        <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ho+j7jyWK8fNQe+A12Hb8AhRq26LrZ/JpcUGGOn+Y7RsweNrtN/tE3MoK7ZeZDyx" crossorigin="anonymous"></script>
    
        <!-- Option 2: jQuery, Popper.js, and Bootstrap JS
        <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
        <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.min.js" integrity="sha384-w1Q4orYjBQndcko6MimVbzY0tgp4pWB4lZ7lr30WKz0vr/aWKhXdBNmNb5D92v7s" crossorigin="anonymous"></script>
        -->
      </body>
    </html>
    ```
  
* Resulting web page

![flask helloworld page](/Images/Flask/flask_1.png)

* Notice that name of tab is changed using this code `<title>Hello, world!</title>`

* We can use more than one routes for same webpage
  ```python
  @app.route("/")   # Decorator
  @app.route("/home")
  def hello_world():
      return render_template("home.html")
  ```
  
***

#### Navigation bar html

Navigation Part inside `body tag` just after `<body>`
```html
<nav class="navbar navbar-expand-md navbar-dark bg-dark">
  <a class="navbar-brand" href="#">Flask Market</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="navbarNav">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
          <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
          <a class="nav-link" href="#">Market</a>
      </li>
    </ul>
    <ul class="navbar-nav">
        <li class="nav-item">
            <a class="nav-link" href="#">Login</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="#">Register</a>
        </li>
    </ul>
  </div>
</nav>
```

Change background color and text color using style tag. `<style>` tag is used inside `<html>` tag alongside `<head>`, `<body>`
```html
<style>
  body{
  background-color: #212121;
  color: white
  }
</style>
```

#### Final home.html page

```html
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css" integrity="sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2" crossorigin="anonymous">

    <title>Home Page</title>
  </head>
  <body>

    <nav class="navbar navbar-expand-md navbar-dark bg-dark">
      <a class="navbar-brand" href="#">Flask Market</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
              <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
          </li>
          <li class="nav-item">
              <a class="nav-link" href="#">Market</a>
          </li>
        </ul>
        <ul class="navbar-nav">
            <li class="nav-item">
                <a class="nav-link" href="#">Login</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="#">Register</a>
            </li>
        </ul>
      </div>
    </nav>

    <h1>Home Page</h1>

    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: jQuery and Bootstrap Bundle (includes Popper) -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ho+j7jyWK8fNQe+A12Hb8AhRq26LrZ/JpcUGGOn+Y7RsweNrtN/tE3MoK7ZeZDyx" crossorigin="anonymous"></script>

    <!-- Option 2: jQuery, Popper.js, and Bootstrap JS
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.min.js" integrity="sha384-w1Q4orYjBQndcko6MimVbzY0tgp4pWB4lZ7lr30WKz0vr/aWKhXdBNmNb5D92v7s" crossorigin="anonymous"></script>
    -->
  </body>

  <style>
    body{
    background-color: #212121;
    color: white
    }
  </style>
</html>
```

Copy `home.html` page contents to `market.html` to create a new page

![Home Page](/Images/Flask/flask_2.png)

***
***

<div id="id3"></div>

### 3) Sending data to templates

#### Sending single data in a variable

Python code
```python
@app.route("/market")
def market_page():
    return render_template("market.html", item_name="Phone")
```

Html code snippet in market.html
```html
<p1>{{ item_name }}</p1>
```

***

#### Sending data in a list of dicts

```python
@app.route("/market")
def market_page():
    items = [
        {'id': 1, 'name': 'Phone', 'barcode': '893212299897', 'price': 500},
        {'id': 2, 'name': 'Laptop', 'barcode': '123985473165', 'price': 900},
        {'id': 3, 'name': 'Keyboard', 'barcode': '231985128446', 'price': 150}
    ]
return render_template("market.html", items=items)
```

>Html snippet
>```html
>    <p1>{{ items }}</p1>
>```
> 
> This gives market page like this (which is not desired)
>```
>Market Page
>[{'id': 1, 'name': 'Phone', 'barcode': '893212299897', 'price': 500}, {'id': 2, 'name': 'Laptop', 'barcode': '123985473165', 'price': 900}, {'id': 3, 'name': 'Keyboard', 'barcode': '231985128446', 'price': 150}]
>```

This is not good. Better to display in a table

***

**Table in HTML - Example**

```html
<table class="table table-hover table-dark">
    <thead>
        <tr>
            <!-- Your Columns HERE -->
            <th scope="col">ID</th>
            <th scope="col">Name</th>
            <th scope="col">Barcode</th>
            <th scope="col">Price</th>
        </tr>
    </thead>
    <tbody>
        <!-- Your rows inside the table HERE: -->
            <tr>
                <td>Value for Id</td>
                <td>Value for Name</td>
                <td>Value for Barcode</td>
                <td>Value for Price</td>
            </tr>
    </tbody>
</table>
```

![Table html using bootstrap](/Images/Flask/flask_3.png)

***

#### Logics inside HTML

jinja allows logics inside html
* To get logics --> `{% %}`
* To get variables --> `{{ variable }}`


* `for loop` syntax
  ```
  {% for index in range(5) %}
      html content
  {% endfor %}
  ```
```html
<table class="table table-hover table-dark">
    <thead>
        <tr>
            <!-- Your Columns HERE -->
            <th scope="col">ID</th>
            <th scope="col">Name</th>
            <th scope="col">Barcode</th>
            <th scope="col">Price</th>
        </tr>
    </thead>
    <tbody>
        <!-- Your rows inside the table HERE: -->
        {% for index in range(5) %}
            <tr>
                <td>{{ index }}</td>
                <td>Value for Name</td>
                <td>Value for Barcode</td>
                <td>Value for Price</td>
            </tr>
        {% endfor %}
    </tbody>
</table>
```

This will display the rows 5 times in a for loop

![Loop in html](/Images/Flask/flask_4.png)
  
**To print the data in list in the table**

dict content can be accessed using `{{ dictName.key }}`

```html
<table class="table table-hover table-dark">
    <thead>
        <tr>
            <!-- Your Columns HERE -->
            <th scope="col">ID</th>
            <th scope="col">Name</th>
            <th scope="col">Barcode</th>
            <th scope="col">Price</th>
        </tr>
    </thead>
    <tbody>
        <!-- Your rows inside the table HERE: -->
        {% for item in items %}
            <tr>
                <td>{{ item.id }}</td>
                <td>{{ item.name }}</td>
                <td>{{ item.barcode }}</td>
                <td>{{ item.price }}</td>
            </tr>
        {% endfor %}
    </tbody>
</table>
```

***

#### Adding `More info` and `Purchase button` for each row

```html
<h1>Market Page</h1>
<table class="table table-hover table-dark">
    <thead>
        <tr>
            <!-- Your Columns HERE -->
            <th scope="col">ID</th>
            <th scope="col">Name</th>
            <th scope="col">Barcode</th>
            <th scope="col">Price</th>
            <th scope="col">Options</th>
        </tr>
    </thead>
    <tbody>
        <!-- Your rows inside the table HERE: -->
        {% for item in items %}
            <tr>
                <td>{{ item.id }}</td>
                <td>{{ item.name }}</td>
                <td>{{ item.barcode }}</td>
                <td>{{ item.price }}</td>
                <td>
                    <button class="btn btn-outline btn-info">More Info</button>
                    <button class="btn btn-outline btn-success">Purchase this Item</button>
                </td>
            </tr>
        {% endfor %}
    </tbody>
</table>
```

* The effects in the table and buttons are provided by the bootstrap classes

![Table with buttons](/Images/Flask/flask_5.png)

***
***

<div id="id4"></div>

### 4) Template Inheritance

* Multiple pages can have same features like nav bar
* In that case, create a feature for one html file and then inherit it in another html file
* This is done using `{% extends 'base.html' %}`


* But in `base.html`, title is `Base Page`. For `home.html` it needs to be 'Home Page'. For this use `block`

  > Put this in base.html
  >```html
  ><title>
  >    {% block title %}
  >      Base Page
  >    {% endblock %}
  ></title>
  >```
  > 
  > Then put this in home.html
  > 
  >```html
  >{% extends 'base.html' %}
  >
  >{% block title %}
  >    Home Page
  >{% endblock %}
  >``` 
  > 
  > `Home Page` in home.html replaces code inside block in base.html


* here `title` is the block name. We can give any name here. Then call this in child html page and replace the parents block body with child's block body


* To make the `Home` and `Market` options in nav bar work, edit href of respective options in `base.html`.
* Use `{{ url_for('home_page') }}` to get url of home page(/home) from python function name

  ```html
  <ul class="navbar-nav mr-auto">
    <li class="nav-item active">
       <a class="nav-link" href="{{ url_for('home_page') }}">Home <span class="sr-only">(current)</span></a>
    </li>
    <li class="nav-item">
       <a class="nav-link" href="{{ url_for('market_page') }}">Market</a>
    </li>
  </ul>
  ```
 
***

#### base.html

```html
<!doctype html>
<html lang="en">
   <head>
      <!-- Required meta tags -->
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
      <!-- Bootstrap CSS -->
      <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css" integrity="sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2" crossorigin="anonymous">
      <title>
          {% block title %}
            Base Page
          {% endblock %}
      </title>
   </head>
   <body>
      <!-- Navbar here -->
      <nav class="navbar navbar-expand-md navbar-dark bg-dark">
         <a class="navbar-brand" href="#">Flask Market</a>
         <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav">
           <span class="navbar-toggler-icon"></span>
         </button>
         <div class="collapse navbar-collapse" id="navbarNav">
           <ul class="navbar-nav mr-auto">
             <li class="nav-item active">
                 <a class="nav-link" href="{{ url_for('home_page') }}">Home <span class="sr-only">(current)</span></a>
             </li>
             <li class="nav-item">
                 <a class="nav-link" href="{{ url_for('market_page') }}">Market</a>
             </li>
           </ul>
           <ul class="navbar-nav">
               <li class="nav-item">
                   <a class="nav-link" href="#">Login</a>
               </li>
               <li class="nav-item">
                   <a class="nav-link" href="#">Register</a>
               </li>
           </ul>
         </div>
      </nav>

      {% block content %}
      {% endblock %}
      <!-- Future Content here -->



      <!-- Optional JavaScript -->
      <!-- jQuery first, then Popper.js, then Bootstrap JS -->
      <script src='https://kit.fontawesome.com/a076d05399.js'></script>
      <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
      <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
      <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js" integrity="sha384-B4gt1jrGC7Jh4AgTPSdUtOBvfO8shuf57BaghqFfPlYxofvL8/KUEfYiJOMMV+rV" crossorigin="anonymous"></script>
   </body>
   <style>
      body {
      background-color: #212121;
      color: white
      }
   </style>
</html>
```

***

#### home.html

```html
{% extends 'base.html' %}

{% block title %}
    Home Page
{% endblock %}

{% block content %}
    <h1>This is the content of Home page</h1>
{% endblock %}
```

***

#### market.html

```html
{% extends 'base.html' %}

{% block title %}
    Market Page
{% endblock %}

{% block content %}
    <table class="table table-hover table-dark">
        <thead>
            <tr>
                <!-- Your Columns HERE -->
                <th scope="col">ID</th>
                <th scope="col">Name</th>
                <th scope="col">Barcode</th>
                <th scope="col">Price</th>
                <th scope="col">Options</th>
            </tr>
        </thead>
        <tbody>
            <!-- Your rows inside the table HERE: -->
            {% for item in items %}
                <tr>
                    <td>{{ item.id }}</td>
                    <td>{{ item.name }}</td>
                    <td>{{ item.barcode }}</td>
                    <td>{{ item.price }}</td>
                    <td>
                        <button class="btn btn-outline btn-info">More Info</button>
                        <button class="btn btn-outline btn-success">Purchase this Item</button>
                    </td>
                </tr>
            {% endfor %}
        </tbody>
    </table>
{% endblock %}
```

***
***

<div id="id5"></div>

### 5) Models & Databases

>Install flask sqlite package
> 
> `pip install flask-sqlalchemy`

> Creating a model
> 
>```python
>from flask import Flask, render_template
>from flask_sqlalchemy import SQLAlchemy
>
>app = Flask(__name__)
>
>app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///market.db"
>db = SQLAlchemy(app)
>
>
>class Item(db.Model):
>    id = db.Column(db.Integer(), primary_key=True)
>    name = db.Column(db.String(length=30), nullable=False, unique=True)
>    price = db.Column(db.Integer(), nullable=False)
>    barcode = db.Column(db.String(length=12), nullable=False, unique=True)
>    description = db.Column(db.String(length=1024), nullable=False, unique=True)
>```
>

***

> **Fetch/Query data from database**
> 
>```python
># For testing only. To create some dummy data in database
># Remove these after testing
>db.create_all()
>item1 = Item(name="Iphone", price=25000, barcode="454879561154", description="Good phone")
>db.session.add(item1)
>db.session.commit()
>print(Item.query.all())  # [<Item 1>]
>
>item2 = Item(name="Laptop", price=55000, barcode="78953458972", description="Good laptop")
>db.session.add(item2)
>db.session.commit()
>print(Item.query.all())  # [<Item 1>, <Item 2>]  -> <modelName id>
>``` 
>
> We can reformat the Item.query.all() by adding this method in class Item
> 
>```python
># To format result of Item.query.all()
>def __repr__(self):
>   return f"Item {self.name}"
>``` 
>
>This will print the result as 
>```
>[Item Iphone]
>[Item Iphone, Item Laptop]
>```
>
>To print all details -
> 
>```python
>for item in Item.query.all():
>    print(str(item.id) + " " + item.name + " " + str(item.price) + " " + str(item.barcode))
>
># 1 Iphone 25000 454879561154
># 2 Laptop 55000 78953458972
>```
>
>**Filter data**
> 
>```python
>for item in Item.query.filter_by(price=55000):
>    print(item.name)  # Laptop
>```

***

#### To display database data in table

```python
@app.route("/market")
def market_page():
    items = Item.query.all()
    return render_template("market.html", items=items)
```

_Full python file_

```python
from flask import Flask, render_template
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)

app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///market.db"
db = SQLAlchemy(app)


class Item(db.Model):
    id = db.Column(db.Integer(), primary_key=True)
    name = db.Column(db.String(length=30), nullable=False, unique=True)
    price = db.Column(db.Integer(), nullable=False)
    barcode = db.Column(db.String(length=12), nullable=False, unique=True)
    description = db.Column(db.String(length=1024), nullable=False, unique=True)


@app.route("/")   # Decorator
@app.route("/home")
def home_page():
    return render_template("home.html")


@app.route("/market")
def market_page():
    items = Item.query.all()
    return render_template("market.html", items=items)
```

NOTE: We can also us sqlbrowser software to view contents of database

***
***

<div id="id6"></div>

### 6) Project Restructure

* move routes to route.py
* move models to models.py
* since different files are interdependent, cyclic imports occur
* So create run.py file which will import different files
* Make market package and create `__init__` file
* `__init__` file has common ones like `app` and `db`
* import necessary ones in respective files
* models is imported in route
* route is imported in `__init__`

![Project Structure](/Images/Flask/flask_6.png)

#### init.py

```python
from flask import Flask, render_template
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///market.db"
db = SQLAlchemy(app)

from market import routes
```

***

#### routes.py

```python
from market import app
from flask import render_template
from market.models import Item


@app.route("/")   # Decorator
@app.route("/home")
def home_page():
    return render_template("home.html")


@app.route("/market")
def market_page():
    items = Item.query.all()
    return render_template("market.html", items=items)
```

***

#### models.py

```python
from market import db


class Item(db.Model):
    id = db.Column(db.Integer(), primary_key=True)
    name = db.Column(db.String(length=30), nullable=False, unique=True)
    price = db.Column(db.Integer(), nullable=False)
    barcode = db.Column(db.String(length=12), nullable=False, unique=True)
    description = db.Column(db.String(length=1024), nullable=False, unique=True)

    def __repr__(self):
        return f"Item {self.name}"
```

***

#### run.py

```python
from market import app

if __name__ == "__main__":
    app.run(debug=True)

```

***
***

<div id="id7"></div>

### 7) Model Relationships

>`items = db.relationship("Item", backref="owned_user", lazy=True)`
> 
>"Item" is class name.
> 
> We can get all items of an user. But to get user from an item like laptop, we need some reference to back track it. So here 'owned-user' can be called to get that details
> 
> `lazy=True` is used to get all items in a single shot
> 

> Note
> 
> db.drop_all()  --> deletes all db contents
> dn.create_all() --> creates db file
> 

#### routes.py with model relationship

```python
from market import db


class User(db.Model):
    id = db.Column(db.Integer(), primary_key=True)
    username = db.Column(db.String(length=30), nullable=False, unique=True)
    email_address = db.Column(db.String(length=50), nullable=False, unique=True)
    password_hash = db.Column(db.String(length=60), nullable=False)
    budget = db.Column(db.Integer(), nullable=False, default=1000)
    items = db.relationship("Item", backref="owned_user", lazy=True)


class Item(db.Model):
    id = db.Column(db.Integer(), primary_key=True)
    name = db.Column(db.String(length=30), nullable=False, unique=True)
    price = db.Column(db.Integer(), nullable=False)
    barcode = db.Column(db.String(length=12), nullable=False, unique=True)
    description = db.Column(db.String(length=1024), nullable=False, unique=True)
    owner = db.Column(db.Integer(), db.ForeignKey("user.id"))

    def __repr__(self):
        return f"Item {self.name}"

```

> **Code to create a dummy user**
> 
> Before creating this, delete database using drop_all() and create using create_all()
> 
>```python
>u1 = User(username="ag", password_hash="123456789", email_address="ag@gmail.com")
>db.session.add(u1)
>db.session.commit()
>
>for user in User.query.all():
>    print(user.username)  # ag
>```
>
>**Now create dummy items**
> 
>```python
>item1 = Item(name="Iphone", price=25000, barcode="454879561154", description="Good phone")
>db.session.add(item1)
>db.session.commit()
>print(Item.query.all())  # [<Item 1>]
>
>item2 = Item(name="Laptop", price=55000, barcode="78953458972", description="Good laptop")
>db.session.add(item2)
>db.session.commit()
>print(Item.query.all())  # [<Item 1>, <Item 2>]  -> <modelName id>
>```
> 
>**Checking owner of an item**
>
>```python
>item1 = Item.query.filter_by(name="Laptop").first()
>print(item1)  # Item Laptop
>print(item1.owner)  # None
>```
>Here there is no owner for this item 'Laptop'. So 'None' is shown
>

***

#### Setting owner of an item

```python
item1 = Item.query.filter_by(name="Laptop").first()
item1.owner = User.query.filter_by(username="ag").first().id
db.session.add(item1)
db.session.commit()
```

Here `id` is used as it is the foreign key

***

#### Getting user object from item object

```python
item1 = Item.query.filter_by(name="Laptop").first()

print(item1.owned_user.username)  # ag
```

***
***

<div id="id8"></div>

### 8) Flask Forms

> `pip install flask-wtf`
> 
> `pip install wtforms`

***

#### form.py

```python
from flask_wtf import FlaskForm
from wtforms import StringField, PasswordField, SubmitField


class RegisterForm(FlaskForm):
    username = StringField(label="User Name:")
    email_address = StringField(label="Email Address:")
    password1 = PasswordField(label="Password:")
    password2 = PasswordField(label="Confirm Password:")
    submit = SubmitField(label="Create Account")


```

***

#### Add this in routes.py

```python
from market.forms import RegisterForm

@app.route("/register")
def register_page():
    form = RegisterForm()
    return render_template("register.html", form=form)
```

***

#### Setting Secret Key

> Create random hex key (We can run this code in terminal python to just get the code)
> 
>```python
>import os
>print(os.urandom(12).hex())  # 'e91f71d2d0e4e1359dd2304b'
>```
>
>Now set it in `__init__.py`
> 
>`app.config["SECRET_KEY"] = "e91f71d2d0e4e1359dd2304b"`

***

#### Editing nav bar Register href in base.html

```html
<li class="nav-item">
   <a class="nav-link" href="{{ url_for('register_page') }}">Register</a>
</li>
```

***

#### register.html

```html
{% extends 'base.html' %}
{% block title %}
Register Page
{% endblock %}

{% block content %}
<body class="text-center">
    <div class="container">
        <form method="POST" class="form-register" style="color:white">
            <h1 class="h3 mb-3 font-weight-normal">
                Please create your Account
            </h1>
            <br>

            {{ form.username.label() }}
            {{ form.username(class="form-control", placeholder="User Name") }}

            {{ form.email_address.label() }}
            {{ form.email_address(class="form-control", placeholder="Email Adddress") }}

            {{ form.password1.label() }}
            {{ form.password1(class="form-control", placeholder="Password") }}

            {{ form.password2.label() }}
            {{ form.password2(class="form-control", placeholder="Confirm Password") }}

            <br>

            {{ form.submit(class="btn btn-lg btn-block btn-primary") }}
        </form>
    </div>
</body>
{% endblock %}
```

>Explanation
> 
> `form.username.label()` is just label text given in form
> 
> `placeholder="User Name"`  displays placeholder text given in respective field
> 
> `{{ form.submit(class="btn btn-lg btn-block btn-primary") }}`
> 
> `btn` --> button, `btn-lg` --> button large, `btn-block`-->expand button to the size of form, `btn-primary`-->gives it blue color
> 

![Flask Form](/Images/Flask/flask_7.png)

***
***

<div id="id9"></div>

### 9) Flask Validations

This section talks about getting user data from user after clicking submit button and store in db

#### Editing routes.py 

```python
from market import app, db
from flask import render_template, redirect, url_for
from market.models import Item, User
from market.forms import RegisterForm

@app.route("/register", methods=["GET", "POST"])
def register_page():
    form = RegisterForm()
    if form.validate_on_submit():
        user_to_create = User(username=form.username.data,
                              email_address=form.email_address.data,
                              password_hash=form.password1.data)
        db.session.add(user_to_create)
        db.session.commit()
        return redirect(url_for("market_page"))
    return render_template("register.html", form=form)
```

>`form.validate_on_submit()` --> returns True when submit button is clicked in form
> 
> `form.username.data` --> gets username entered by user in webpage to backend
> 
> `methods=["GET", "POST"]`  --> since we are using these methods here (POST)

***

#### Cross Site Request Forgery(CSRF)

This is an attack towards database to do some unwanted actions. To protect from this attack, use this-

> Edit form tag in register.html page
> 
>```html
><form method="POST" class="form-register" style="color:white">
>       {{ form.hidden_tag() }}
>```

***

#### Adding wtforms.validators in forms.py

```python
from flask_wtf import FlaskForm
from wtforms import StringField, PasswordField, SubmitField
from wtforms.validators import Length, EqualTo, Email, DataRequired


class RegisterForm(FlaskForm):
    username = StringField(label="User Name:", validators=[Length(min=2, max=30), DataRequired()])
    email_address = StringField(label="Email Address:", validators=[Email(), DataRequired()])
    password1 = PasswordField(label="Password:", validators=[Length(min=6), DataRequired()])
    password2 = PasswordField(label="Confirm Password:", validators=[EqualTo("password1"), DataRequired()])
    submit = SubmitField(label="Create Account")
```

* `DataRequired()`  -> This field in mandatory
* `Length()` -> Length of characters must be..
* `EqualTo("anotherfield")`  -> this field must be equal to another field

* `Email()`-> checks if this is valid email address. To use this, install email_validator `pip install email_validator`

***

#### Viewing validation errors in terminal of server

* We add a `form.errors` condition to print errors

```python
@app.route("/register", methods=["GET", "POST"])
def register_page():
    form = RegisterForm()
    if form.validate_on_submit():
        user_to_create = User(username=form.username.data,
                              email_address=form.email_address.data,
                              password_hash=form.password1.data)
        db.session.add(user_to_create)
        db.session.commit()
        return redirect(url_for("market_page"))
    if form.errors != {}:
        for err_msg in form.errors.values():
            print(f"Error occurred when creating a user: {err_msg}")
    return render_template("register.html", form=form)
```

* Now we give incorrect data in webpage like single chara username, invaid email, mismatching passwords

* length erros we get it in ui itself

> server terminal error messages
> 
> ```
>Error occurred when creating a user: ['Invalid email address.']
>Error occurred when creating a user: ['Field must be equal to password1.']
>```

***
***

<div id="id10"></div>

### 10) Flash messages & Advanced Validations

* Instead of printing errors in terminal, flash it in ui
* This is done by adding some codes in routes.py and base.html

#### Edit routes.py

`from flask import render_template, redirect, url_for, flash`

```python
if form.errors != {}:
    for err_msg in form.errors.values():
        flash(f"Error occurred when creating a user: {err_msg}")
```

***

#### Edit base.html

* This is added before block content created earlier

```html
{% with messages = get_flashed_messages(with_categories=true) %}
  {% if messages %}
      {% for message in messages %}
          <p>{{ message }}</p>
      {% endfor %}
  {% endif %}
{% endwith %}

{% block content %}
{% endblock %}
<!-- Future Content here -->
```

![Flashed messages](/Images/Flask/flask_8.png)

>`('message', "Error occurred when creating a user: ['Invalid email address.']")`
> 
> Here first one is category and second one is the message


> To display only message and not category, edit code in base.html as:
> 
>```html
>{% for category, message in messages %}
>            <p>{{ message }}</p>
>        {% endfor %}
>```

***

#### To display message like an alert with close button X

> Edit in routes.py
> 
>```python
>flash(f"Error occurred when creating a user: {err_msg}", category="danger")
>```
> 
> Edit in base.html
> 
>```html
>{% with messages = get_flashed_messages(with_categories=true) %}
>  {% if messages %}
>      {% for category, message in messages %}
>          <div class="alert alert-{{ category }}">
>              <button type="button" class="m1-2 mb-1 close" data-dismiss="alert" aria-label="Close">
>                  <span aria-hidden="true">&times;</span>
>              </button>
>              {{ message }}
>          </div>
>      {% endfor %}
>  {% endif %}
>{% endwith %}
>
>{% block content %}
>{% endblock %}
><!-- Future Content here -->
>``` 

![Alert message](/Images/Flask/flask_9.png)

***

#### Giving username which is already present in DB

* Giving already existing username to create account, gives an error

  ```
  IntegrityError
  sqlalchemy.exc.IntegrityError: (sqlite3.IntegrityError) UNIQUE constraint failed: user.username
  [SQL: INSERT INTO user (username, email_address, password_hash, budget) VALUES (?, ?, ?, ?)]
  ```
  
* Edit forms.py to give a validation error when existing username or email is used again

```python
from flask_wtf import FlaskForm
from wtforms import StringField, PasswordField, SubmitField
from wtforms.validators import Length, EqualTo, Email, DataRequired, ValidationError
from market.models import User


class RegisterForm(FlaskForm):

    # method name should be starting with 'validate_' + <field name exactly>
    # Then FlaskForm(parent class) will automatically calls this method
  
    def validate_username(self, username_to_check):
        user = User.query.filter_by(username=username_to_check.data).first()
        if user:
            raise ValidationError("Username already exists! Please try  a different username")

    def validate_email_address(self, email_address_to_check):
        user = User.query.filter_by(email_address=email_address_to_check.data).first()
        if user:
            raise ValidationError("Email Address already exists! Please try  a different email address")

    username = StringField(label="User Name:", validators=[Length(min=2, max=30), DataRequired()])
    email_address = StringField(label="Email Address:", validators=[Email(), DataRequired()])
    password1 = PasswordField(label="Password:", validators=[Length(min=6), DataRequired()])
    password2 = PasswordField(label="Confirm Password:", validators=[EqualTo("password1"), DataRequired()])
    submit = SubmitField(label="Create Account")
```

Now this will show validation errors

***
***

<div id="id11"></div>

### 11) User Authentication

#### Encrypting password

> `pip install flask-bcrypt`

> **Add these in init.py** 
> 
>```python
>from flask_bcrypt import Bcrypt
>bcrypt = Bcrypt(app)
>```
>
> ***
>
>**Modify User in models.py to set password property**
> 
>```python
>from market import db, bcrypt
>
>class User(db.Model):
>    id = db.Column(db.Integer(), primary_key=True)
>    username = db.Column(db.String(length=30), nullable=False, unique=True)
>    email_address = db.Column(db.String(length=50), nullable=False, unique=True)
>    password_hash = db.Column(db.String(length=60), nullable=False)
>    budget = db.Column(db.Integer(), nullable=False, default=1000)
>    items = db.relationship("Item", backref="owned_user", lazy=True)
>
>    @property
>    def password(self):
>        return self.password
>
>    @password.setter
>    def password(self, plain_text_password):
>        self.password_hash = bcrypt.generate_password_hash(plain_text_password).decode('utf-8')
>
>```
>
>***
> 
> **Edit password_hash to password in routes.py register_page method**
> 
>```python
>user_to_create = User(username=form.username.data,
>                      email_address=form.email_address.data,
>                      password=form.password1.data)
>```
>
>Now password will be encrypted and stored in db
> 

***

#### User Login

> **Create method in routes.py**
> 
>```python
>@app.route("/login", methods=["GET", "POST"])
>def login_page():
>    form = LoginForm()
>    return render_template("login.html", form=form)
>```
>
>
> **Set Login page in nav bar in base.html**
> 
>```html
> <li class="nav-item">
>   <a class="nav-link" href="{{ url_for('login_page') }}">Login</a>
> </li>
>```
> 
>
> **Create Login Form in forms.py**
> 
>```python
>class LoginForm(FlaskForm):
>    username = StringField(label="User Name:", validators=[DataRequired()])
>    password = PasswordField(label="Password:", validators=[DataRequired()])
>    submit = SubmitField(label="Sign in")
>```
> 

#### login.html

```html
{% extends 'base.html' %}
{% block title %}
    Login Page
{% endblock %}

{% block content %}
<body class="text-center">
    <div class="container">
        <form method="POST" class="form-signin" style="color:white">
            {{ form.hidden_tag() }}
            <h1 class="h3 mb-3 font-weight-normal">
                Please Login
            </h1>
            <br>
            {{ form.username.label() }}
            {{ form.username(class="form-control", placeholder="User Name") }}

            {{ form.password.label() }}
            {{ form.password(class="form-control", placeholder="Password") }}

            <br>


            <div class="checkbox mb-3">
               <h6>Do not have an account?</h6>
               <a class="btn btn-sm btn-secondary" href="{{ url_for('register_page') }}">Register</a>
            </div>

            {{ form.submit(class="btn btn-lg btn-block btn-primary") }}

        </form>
    </div>
</body>
{% endblock %}
```

> **NOTE**
> 
> We can give a provision in register page for already registered user to login by adding this snippet in register.html like in login.html
> 
>```html
><div class="checkbox mb-3">
>   <h6>Already have an account?</h6>
>   <a class="btn btn-sm btn-secondary" href="{{ url_for('login_page') }}">Log in</a>
></div>
>```
>

***

#### LOGIN Authentication - Main Part
