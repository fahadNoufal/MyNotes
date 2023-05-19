A Django template is a text document or a Python string marked-up using the Django template language.
Some constructs are recognized and interpreted by the template engine. The main ones are variables and tags.


## Variables
is a dict-like object mapping keys to values.

`Variables are surrounded by `{{` and `}}` like this:`
My first name is {{ first_name }}. My last name is {{ last_name }}.

With a context of `{'first_name': 'John', 'last_name': 'Doe'}`, this template renders to:

My first name is John. My last name is Doe.

## Tags

Tags provide arbitrary logic in the rendering process.

A tag can output content, serve as a control structure e.g. an “if” statement or a “for” loop, grab content from a database, or even enable access to other template tags.

Tags are surrounded by `{%` and `%}` like this:
`{% csrf_token %}`
`{% if user.is_authenticated %}Hello, {{ user.username }}.
`{% endif %}`

## Filters
Filters transform the values of variables and tag arguments.

They look like this:
	`{{ django|title }}`

With a context of `{'django':'the web framework for perfectionists with deadlines'}`, 
this template renders to:
	The Web Framework For Perfectionists With Deadlines

Some filters take an argument:
``	{{ my_date|date:"Y-m-d" }}

### {\% include 'navbar.html' %}
ths will include the navbar.html in the place where you place
### {\% block content %} { \% endblock content%}
creates a block where you can add other templates
To use these blocks you need to include the main file where the blocks should be placed
### {\% extends 'main.html' %}

## Comments

Comments look like this:
{# this won't be rendered #}
A `{%comment %}` tag provides multi-line comments.


# Configuration

Templates engines are configured with the [`TEMPLATES`](https://docs.djangoproject.com/en/4.1/ref/settings/#std-setting-TEMPLATES) setting.
It’s a list of configurations, one for each engine.

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [
	        BASE_DIR / 'templates'
        ],
        'APP_DIRS': True,
        'OPTIONS': {
            # ... some options here ...
        },
    },
]
```

[`BACKEND`](https://docs.djangoproject.com/en/4.1/ref/settings/#std-setting-TEMPLATES-BACKEND) is a dotted Python path to a template engine class implementing Django’s template backend API. The built-in backends are [`django.template.backends.django.DjangoTemplates`](https://docs.djangoproject.com/en/4.1/topics/templates/#django.template.backends.django.DjangoTemplates "django.template.backends.django.DjangoTemplates") 

[`DIRS`](https://docs.djangoproject.com/en/4.1/ref/settings/#std-setting-TEMPLATES-DIRS) defines a list of directories where the engine should look for template source files, in search order.

[`APP_DIRS`](https://docs.djangoproject.com/en/4.1/ref/settings/#std-setting-TEMPLATES-APP_DIRS) tells whether the engine should look for templates inside installed applications. Each backend defines a conventional name for the subdirectory inside applications where its templates should be stored.


