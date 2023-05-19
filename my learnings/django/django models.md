A model is the single, definitive source of information about your data. It contains the essential fields and behaviors of the data you’re storing. Generally, each model maps to a single database table.

The basics:

-   Each model is a Python class that subclasses [`django.db.models.Model`](https://docs.djangoproject.com/en/4.1/ref/models/instances/#django.db.models.Model "django.db.models.Model").
-   Each attribute of the model represents a database field.
-   With all of this, Django gives you an automatically-generated database-access API

import django user model
`from django.contrib.auth.models import User`

## Fields

The most important part of a model – and the only required part of a model – is the list of database fields it defines. 
Fields are specified by class attributes.

```python
from django.db import models

class Musician(models.Model):
    first_name = models.CharField(max_length=50)
    last_name = models.CharField(max_length=50)
    instrument = models.CharField(max_length=100)

class Album(models.Model):
    artist = models.ForeignKey(Musician, 
							    on_delete=models.CASCADE)
    name = models.CharField(max_length=100)
    release_date = models.DateField()
    num_stars = models.IntegerField()

	class Meta:
		ordering=['-release_date']

```

Each field takes a certain set of field-specific arguments
For example `CharField`  requires a `max_length` argument which specifies the size

There’s also a set of common arguments available to all field types.

#### 1. null
If `True`, Django will store empty values as `NULL` in the database. Default is `False`.

#### 2. blank
If `True`, the field is allowed to be blank. Default is `False`.

Note that this is different than [`null`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.Field.null "django.db.models.Field.null"). [`null`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.Field.null "django.db.models.Field.null") is purely database-related, whereas [`blank`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.Field.blank "django.db.models.Field.blank") is validation-related. If a field has [`blank=True`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.Field.blank "django.db.models.Field.blank"), form validation will allow entry of an empty value. If a field has [`blank=False`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.Field.blank "django.db.models.Field.blank"), the field will be required

#### 3. choices
A [sequence](https://docs.python.org/3/glossary.html#term-sequence "(in Python v3.11)") of 2-tuples to use as choices for this field. If this is given, the default form widget will be a select box instead of the standard text field and will limit choices to the choices given.

A choices list looks like this:
```python
YEAR_IN_SCHOOL_CHOICES = [
    ('FR', 'Freshman'),
    ('SO', 'Sophomore'),
    ('JR', 'Junior'),
    ('SR', 'Senior'),
    ('GR', 'Graduate'),
]
```

The first element in each tuple is the value that will be stored in the database. The second element is displayed by the field’s form widget.
![[Pasted image 20230505114001.png]]

#### 4. primary_key
If `True`, this field is the primary key for the model.

if you don’t specify [`primary_key=True`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.Field.primary_key "django.db.models.Field.primary_key") for any fields in your model, Django will automatically add an [`IntegerField`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.IntegerField "django.db.models.IntegerField") to hold the primary key, so you don’t need to set [`primary_key=True`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.Field.primary_key "django.db.models.Field.primary_key") on any of your fields unless you want to override the default primary-key behavior.

If Django sees you’ve explicitly set [`Field.primary_key`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.Field.primary_key "django.db.models.Field.primary_key"), it won’t add the automatic `id` column.(auto-incrementing primary key)

#### 5. default
The default value for the field. This can be a value or a callable object. If callable it will be called every time a new object is created.

#### 6. unique
If `True`, this field must be unique throughout the table.

# Verbose field names

Each field type, except for [`ForeignKey`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.ForeignKey "django.db.models.ForeignKey"), [`ManyToManyField`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.ManyToManyField "django.db.models.ManyToManyField") and [`OneToOneField`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.OneToOneField "django.db.models.OneToOneField"), takes an optional first positional argument – a verbose name. If the verbose name isn’t given, Django will automatically create it using the field’s attribute name, converting underscores to spaces.

`In this example, the verbose name is "person's first name":
first_name = models.CharField("person's first name", max_length=30)

`In this example, the verbose name is "first name":
first_name = models.CharField(max_length=30)

[`ForeignKey`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.ForeignKey "django.db.models.ForeignKey"), [`ManyToManyField`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.ManyToManyField "django.db.models.ManyToManyField") and [`OneToOneField`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.OneToOneField "django.db.models.OneToOneField") require the first argument to be a model class, so use the [`verbose_name`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.Field.verbose_name "django.db.models.Field.verbose_name") keyword argument:

```python
poll = models.ForeignKey(
    Poll,
    on_delete=models.CASCADE,
    verbose_name="the related poll",
)
sites = models.ManyToManyField(Site, verbose_name="list of sites")
```

## To save the models
type command:
`python manage.py makemigrations`
`python manage.py migrate`

### To view the migrations on admin pannel
go to admin.py
```python
from .models import Room

admin.site.register(Room)
```

[[Django models relationships]]