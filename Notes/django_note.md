# Django

## Table of Contents
1) [Start Project](#id1)
2) [Runs Server](#id2)
3) [Sync settings with django project](#id3)
4) [Admin login](#id4)
5) [Start apps](#id5)
6) [Adding models](#id6)

### Install django
```pip install django```

***

<div id="id1"></div>

### 1) Start Project
```commandline
django-admin startproject projectname
```
```
RESULTANT FOLDER STRUCTURE

-projectname
        -asgi.py
        -settings.py
        -urls.py
        -wsgi.py
        -__init__.py
-db.sqlite3
-manage.py
```

***

<div id="id2"></div>

### 2) Runs Server
``` 
python manage.py runserver
```

***

<div id="id3"></div>

### 3) Sync settings with django project

```commandline
python .\manage.py migrate
```

***

<div id="id4"></div>

### 4) Admin login

In settings, we have installed apps
> INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]

Let's try admin..

go to url `http://127.0.0.1:8000/admin/`

#### Create superuser (Super Admin)

```
python manage.py createsuperuser
```
enter username, email(optional), password to create account

try it in website..

Now admin can add users with name and email and do other stuffs in the website itself

***

<div id="id5"></div>

### 5) Start apps

```commandline
 python manage.py startapp appname 
```

Used to create different apps as required.

> Inside appname folder in root ( same location as manage.py)
> 
>        -migrations
>               -__init__.py
>        -admin.py
>        -apps.py
>        -models.py
>        -tests.py
>        -views.py
>        -__init__.py

***

<div id="id6"></div>

### 6) Adding models

* Write a new model/class in model.py file, in appname
    ```python
    class Product(models.Model):
        name = models.TextField()
        description = models.TextField()
    
    ```

* Then execute following commands

    `python manage.py makemigrations`
    `python manage.py migrate`

  
* If new fields are added in model after doing these, we need to put default value also
    ```python
    summary = models.TextField(default="Default text, enter something")
    ```
    Execute both migration commands after changing models

* Then register these models in admin site
    ```python
    # my imports
    from .models import Product
    
    # Register your models here.
    admin.site.register(Product)
    ```

* Also add app name(ex: products) in settings file installed app list

    >INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'products',
    ]

* Now visit url for testing these `http://127.0.0.1:8000/admin/`


![product object added image](../Codes/django_learnings/images/django_products_1.png)

#### Creating product objects using shell

* Start shell in command line
`python manage.py shell`

* Import the `Product` class we created 
```python
from products.models import Product
```

* To see all objects of the class created till now
`Product.objects.all()`

* To create a new object for 'Product' class
```python
Product.objects.create(name='productName',description='some Description',summary='Some Summary')
```
* Product object gets updated in site

![model object added](../Codes/django_learnings/images/django_products_2.png)

***

###
