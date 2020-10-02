## Django (Urls and Views)

# URLs?

![Difference uri and urls](https://res.cloudinary.com/practicaldev/image/fetch/s--lrbx3qNQ--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/j4bka41nypm4do1f3e5b.JPG)


# URLs in django
##### urls.py
```python
from django.urls import path
from .views import index, profile

app_name = "home"

urlpatterns = [
    path('/', index, name='home'),
    path('profile/', profile, name='profile'),
]
```


# Views?
##### views.py
```python
from django.shortcuts import render

def index(request):
    return render(request, 'index.html')

def profile(request):
    return render(request, 'profile.html')
```

# interaction between views and template

### basic django templating

##### views.py
```python
from django.shortcuts import render

def index(request):
    return render(request, 'index.html', {"coba" : "Hello World"})

def profile(request):
    return render(request, 'profile.html')
```
##### index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
  ...
</head>
<body>
    {{ coba }}
</body>
</html>
```

### if else

##### views.py
```python
from django.shortcuts import render

def index(request):
    return render(request, 'index.html', 
            {
                "condition" : False,
                "coba" : "harusnya ga muncul",
                "coba2" : "harusnya muncul",
            })

def profile(request):
    return render(request, 'profile.html')
```
##### index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
  ...
</head>
<body>
    { %  if condition  % }
        {{ coba }}
    { %  else  % }
        {{ coba2 }}
    { %  endif  % }
</body>
</html>
```
###### tips: don't forget to place "{ %  endif  % }" to tell django that you have closed the if statement

### looping

##### views.py
```python
from django.shortcuts import render

def index(request):
    return render(request, 'index.html', {"mylist" : ["a", "b", "c"]})

def profile(request):
    return render(request, 'profile.html')
```
##### index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
  ...
</head>
<body>
    { %  for data in mylist  % }
        {{ data }}
    { %  endfor  % }
</body>
</html>
```
###### tips: don't forget to place "{ %  endfor  % }" to tell django that you have closed the for loop

#### you can play with json-like object or dictionary
##### views.py
```python
from django.shortcuts import render

def index(request):
    return render(request, 'index.html', 
                {"peeps" : [
                    {"name" : "siapa", "id" : 123, "age" : 19},
                    {"name" : "siapa2", "id" : 124, "age" : 21},
                    {"name" : "siapa3", "id" : 122, "age" : 18},
                    ]
                }
            )

def profile(request):
    return render(request, 'profile.html')
```
##### index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
  ...
</head>
<body>
    { % for people in peeps  % }
        <h1> name: {{ people.name }} </h1>
        <h2> id: {{ people.id }}</h2>
        <h3> age: {{ people.age }}</h3>
    { %  endfor  % }
</body>
</html>
```

### models
---
```python
from django.db import models

class myProfile(models.Model):
    username = models.CharField(max_length=25)
    email = models.EmailField(max_length=100)
```

Table namaapp_myProfile

| id | username    | email                 |
|----|-------------|-----------------------|
| 1  | coba        | coba2@gmail.com       |
| 2  | coba2       | coba2@gmail.com       |

#### melihat models lewat shell
---
jangan lupa untuk memigrasi tabel yang sudah dibuat
```bash
python manage.py makemigrations
python manage.py migrate
```

membuka shell untuk project django
```bash
$ python manage.py shell
```
lalu akan ada tampilan seperti shell pada python

```bash
Python 3.6.8 (default, Jan 14 2019, 11:02:34)
[GCC 8.0.1 20180414 (experimental) [trunk revision 259383]] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

import class yang sudah di buat tadi di dalam folder app
```python
>>> from app.models import myProfile
```

membuat object dari model yang sudah dibuat

```python
>>> myProfile(username='coba', email='coba@gmail.com').save()
>>> myProfile(username='coba2', email='coba2@gmail.com').save()
```

query class yang sudah dibuat 
```python
>>> myProfile.objects.all()
<QuerySet [<myProfile: myProfile object (1)>, <myProfile: myProfile object (2)>]>
```

lihat attribut2 dari tiap2 object yang sudah dibuat
```python
>>> myProfile.objects.all().values()
<QuerySet [{'id': 1, 'username': 'coba', 'email': 'coba@gmail.com'}, {'id': 2, 'username': 'coba2', 'email': 'coba2@gmail.com'}]>
```

mendefinisikan to string pada sebuah model django (sama seperti class biasa)
```python
from django.models import models

class myProfile(models.Model):
    username = models.CharField(max_length=25)
    email = models.EmailField(max_length=100)

    def __str__(self):
        return "{}: {}".format(self.username, self.email)
```

maka melihat query akan lebih mudah
###### best practice nya kalian mendefinisikan method \__str__() sendiri
```python
>>> myProfile.objects.all()
<QuerySet [<myProfile: coba: coba@gmail.com>, <myProfile: coba2: coba2@gmail.com>]>
```

macam - macam field django
###### diambil dari https://www.geeksforgeeks.org/django-model-data-types-and-fields-list/
basic data types

| Field Name    | Description                                                                                                          |
|---------------|----------------------------------------------------------------------------------------------------------------------|
| BooleanField  | A true/false field.The default form widget for this field is a CheckboxInput.                                        |
| CharField     | It is a date, represented in Python by a datetime.date instance.                                                     |
| DateField     | A date, represented in Python by a datetime.date instance                                                            |
| DateTimeField | It is used for date and time, represented in Python by a datetime.datetime instance.                                 |
| EmailField    | It is a CharField that checks that the value is a valid email address.                                               |
| FileField     | It is a file-upload field.                                                                                           |
| ImageField    | It inherits all attributes and methods from FileField, but also validates that the uploaded object is a valid image. |
| TextField     | A large text field. The default form widget for this field is a Textarea.                                            |

more : https://docs.djangoproject.com/en/2.2/ref/models/fields/#field-types

relationship fields

| Field name      | Description                                                                                                                                                                                               |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ForeignKey      | A many-to-one relationship. Requires two positional arguments: the class to which the model is related and the on_delete option.                                                                          |
| ManyToManyField | A many-to-many relationship. Requires a positional argument: the class to which the model is related, which works exactly the same as it does for ForeignKey, including recursive and lazy relationships. |
| OneToOneField   | A one-to-one relationship. Conceptually, this is similar to a ForeignKey with unique=True, but the “reverse” side of the relation will directly return a single object.                                   |

more : https://docs.djangoproject.com/en/2.2/ref/models/fields/#module-django.db.models.fields.related