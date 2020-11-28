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
    {\%  if condition  \%}
      {{ coba }}
    {\%  else  \%}
      {{ coba2 }}
    {\%  endif  \%}
</body>
</html>
```
###### tips: don't forget to place "{\%  endif  \%}" to tell django that you have closed the if statement

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
    {\%  for data in mylist  \%}
        {{ data }}
    {\%  endfor  \%}
</body>
</html>
```
###### tips: don't forget to place "{\%  endfor  \%}" to tell django that you have closed the for loop

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
    {\% for people in peeps  \%}
        <h1> name: {{ people.name }} </h1>
        <h2> id: {{ people.id }}</h2>
        <h3> age: {{ people.age }}</h3>
    {\%  endfor  \%}
</body>
</html>
```

