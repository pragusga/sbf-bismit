# Django - Models

## Outline
* Django Models
  * [Membuat Class pada `models.py`](#membuat-class-pada-homepagemodelspy)
  * [Mendaftarkan Class pada `admin.py`](#mendaftarkan-class-pada-homepageadminpy)
  * [Django CRUD (Create, Read, Update, Delete)](#Django-CRUD)
    * [Membuat Objek baru](#membuat-object-dari-model-yang-sudah-dibuat)
    * [Melihat Objek](#melihat-objek)
    * [Mengedit Objek](#mengedit-objek)
    * [Menghapus Objek](#menghapus-objek)
  * [Tabel Tipe Data](#tabel-tipe-data)
  * [Relationship Fields](#tabel-jenis-jenis-relationship-)

Membuat Class pada `homepage/models.py`
---
```python
from django.db import models

class myProfile(models.Model):
    username = models.CharField(max_length=25)
    email = models.EmailField(max_length=100)
```

Table homepage_myProfile

| id | username    | email                 |
|----|-------------|-----------------------|
| 1  | coba        | coba2@gmail.com       |
| 2  | coba2       | coba2@gmail.com       |

Mendaftarkan Class pada `homepage/admin.py`
---
Untuk membuat model dalam admin Django, kita perlu memodifikasi `homepage/admin.py`. Buka `admin.py` di homepage dan masukkan kode berikut. Impor model terkait dari `models.py` dan daftarkan ke antarmuka admin.

```python
from django.contrib import admin  
    
# Register your models here.  
from .models import myProfile  
    
admin.site.register(myProfile)  
```

### Melihat models lewat shell
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

Membuat object dari model yang sudah dibuat
---
```python
>>> myProfile(username='coba', email='coba@gmail.com').save()
>>> myProfile(username='coba2', email='coba2@gmail.com').save()
```

Melihat objek
---
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

Mengedit objek
---
```python
>>> obj1 = myProfile.objects.get(id=1) #username:coba
>>> obj1.username = "cobaEdited"
>>> obj1.save()
```

Menghapus objek
---
```python
>>> obj2 = myProfile.onjects.get(id=2)
>>> obj2.delete()
```

Tabel tipe data
---
macam - macam field django diambil dari https://www.geeksforgeeks.org/django-model-data-types-and-fields-list/
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

Tabel jenis-jenis relationship 
---
| Field name      | Description                                                                                                                                                                                               |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ForeignKey      | A many-to-one relationship. Requires two positional arguments: the class to which the model is related and the on_delete option.                                                                          |
| ManyToManyField | A many-to-many relationship. Requires a positional argument: the class to which the model is related, which works exactly the same as it does for ForeignKey, including recursive and lazy relationships. |
| OneToOneField   | A one-to-one relationship. Conceptually, this is similar to a ForeignKey with unique=True, but the “reverse” side of the relation will directly return a single object.                                   |

more : https://docs.djangoproject.com/en/2.2/ref/models/fields/#module-django.db.models.fields.related