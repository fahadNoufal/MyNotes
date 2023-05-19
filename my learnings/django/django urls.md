When a user requests a page from your Django-powered site, this is the algorithm the system follows to determine which Python code to execute:

1. Django determines the root URLconf module to use.
2. Django loads that Python module and looks for the variable `urlpatterns`. This should be a sequence of `django.urls.path()`
3. 1.  Django runs through each URL pattern, in order, and stops at the first one that matches the requested URL, matching against `path_info
4. Once one of the URL patterns matches, Django imports and calls the given view, which is a Python function (or a [class-based view](https://docs.djangoproject.com/en/4.1/topics/class-based-views/)). The view gets passed the following arguments:
   -   An instance of `HttpRequest`
   -   If the matched URL pattern contained no named groups, then the matches from the regular expression are provided as positional arguments.
   - 1.  -   The keyword arguments are made up of any named parts matched by the path expression that are provided, overridden by any arguments specified in the optional `kwargs` argument to [`django.urls.path()`](https://docs.djangoproject.com/en/4.1/ref/urls/#django.urls.path "django.urls.path") or [`django.urls.re_path()`](https://docs.djangoproject.com/en/4.1/ref/urls/#django.urls.re_path "django.urls.re_path").
5. If no URL pattern matches, or if an exception is raised during any point in this process, Django invokes an appropriate error-handling view.

eg:
```python
from django.urls import path

from . import views

urlpatterns = [
    path('articles/2003/', views.special_case_2003),
    path('articles/<int:year>/', views.year_archive),
    path('articles/<int:year>/<int:month>/', views.month_archive),
    path('articles/<int:year>/<int:month>/<slug:slug>/', views.article_detail),
]
```

in views
```python
def article(request,year):
```

Notes:

-   To capture a value from the URL, use angle brackets.
-   Captured values can optionally include a converter type. For example, use `<int:name>` to capture an integer parameter. If a converter isn’t included, any string, excluding a `/` character, is matched.
-   There’s no need to add a leading slash, because every URL has that. For example, it’s `articles`, not `/articles`.

Example requests:

-   A request to `/articles/2005/03/` would match the third entry in the list. Django would call the function `views.month_archive(request, year=2005, month=3)`.
-   `/articles/2003/` would match the first pattern in the list, not the second one, because the patterns are tested in order, and the first one is the first test to pass. Feel free to exploit the ordering to insert special cases like this. Here, Django would call the function `views.special_case_2003(request)`
-   `/articles/2003` would not match any of these patterns, because each pattern requires that the URL end with a slash.
-   `/articles/2003/03/building-a-django-site/` would match the final pattern. Django would call the function `views.article_detail(request, year=2003, month=3, slug="building-a-django-site")`.


## Path converters

The following path converters are available by default:

-   `str` - Matches any non-empty string, excluding the path separator, `'/'`. This is the default if a converter isn’t included in the expression.
-   `int` - Matches zero or any positive integer. Returns an `int`.
-   `slug` - Matches any slug string consisting of ASCII letters or numbers, plus the hyphen and underscore characters. For example, `building-your-1st-django-site`.
-   `uuid` - Matches a formatted UUID. To prevent multiple URLs from mapping to the same page, dashes must be included and letters must be lowercase. For example, `075194d3-6885-417e-a8a8-6c931e272f00`. Returns a [`UUID`](https://docs.python.org/3/library/uuid.html#uuid.UUID "(in Python v3.11)") instance.
-   `path` - Matches any non-empty string, including the path separator, `'/'`. This allows you to match against a complete URL path rather than a segment of a URL path as with `str`.