create your app by
`python manage.py startapp <appname>`

connect the app to the installed_apps in settings.py
in settings.py
```python
INSTALLED_APPS=[
	.....,
	'base.apps.BaseConfig'
	#base here is the name of the app
]
```

create your views in views.py in your app

in base/views.py
```python
from django.shortcuts import render
from django.http import HttpResponse

def home(request):
	return HttpResponse('Home Page')

def room(request):
	return render(request,'room.html',{'rooms':rooms})
```

Create the url.py file 
in urls.py
```python 
from django.urls import path
from . import views

urlpatterns=[
	path('',views.home,name='home'),
	path('room/',views.room,name='room')
]
```

Then connect this urls to the urls in the main folder
go to project/urls.py
```python
from django.urls import path,include
urlpatterns=[
	...,
	path('',include('base.urls'))
	# here we connect to <appName>/urls
]
```

## Templates inside app
templates inside the app must be in a folder named templates
and in that template create a subfolder giving the same name as the app and then store templates inside that subfolder

eg : if 'base' is the name of the app
then store the templates inside
`base/templates/base`
