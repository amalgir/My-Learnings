# Python Flask 

## Table of Contents
1) [Introduction](#id1)
2) [Styling & Templates](#id2)
3) [Sending data to templates](#id3)
4) [Template Inheritance](#id4)

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
