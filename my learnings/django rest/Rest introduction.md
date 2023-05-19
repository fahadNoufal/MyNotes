A non api regular request will give you HTML ,while on the other hand REST API HTTP REQUEST wil send JSON data

if it is a JSON response , we can run 
```python
import requests
endpoint = 'https://httpbin.org/anything'
http_response = requests.get(endpoint)

print(http_response.json())
```
`.json()`  will convert the JSON response into `python` Dictonary

## Create a basic django api endpoint

1. Create an app and go to views.py
   
```python
from django.http import JsonResponse

def api_home(request):
	return JsonResponse(
		{'message':'Hello , How are you ?'}
	)
```

2. create a url for this view , connect it to settings.py and runserver

3. Access this endpoint with python 

```python
import requests
endpoint = 'http://localhost:8000/api/'
http_response = requests.get(endpoint)
print(http_response.json())
```

## Echo back Get data 
return back the data that we are sending

```python
import json
from django.http import JsonResponse

def api_home(request):

	body=request.body 
	#returns back byte string (stringified) of json data
	data={}
	try:
		data=json.loads(body)
		# turns : string of Json data -> python dict
	except:
		pass
	print(data)
	
	# We can also assign 
	data['content_type']=request.content_type 
	data['params']=dict(request.GET )# have to convert
	# returns url query params
	# can also use to extract post data	
	return JsonResponse(
		data
	)
```

## Django model instance to python dict

```python
from django.forms.models import model_to_dict
from .models import Products

def api_home(request):
	product=Products.objects.all().order_by('?').first()
	data={}
	if product :
		data['name']=product.name
		data['description']=product.description
		data['price']=product.price
		# Instead of all these, we can convert a model into a dictionary just by using 'model_to_dict' method
		data=model_to_dict(product)	
		# if you want to specify fields which the data should contain , you could add it by using 'feild=' arg
		data=model_to_dict(product,feild=['id','name'])
		# now the data will only contain id and name key instead of all the feilds in 'product'
	return JsonResponse(data)
```

#### HttpResponse & JsonResponse
The main difference b/w these two are that the `JsonResponse accepts dictonary as an argument` 
while `HttpResponse` returns `content_type='text/html'`

# Rest Framework view &   response

this is our code without rest_framework:
```python
def api_home(request):
	product=Products.objects.all().order_by('?').first()
	data={}
	if product :
		data=model_to_dict(product,feild=['id','name'])
	return JsonResponse(data)
```

To convert it into django:
```python
from rest_framework.response import Response
from rest_framework.decorators import api_view

 # with this, it will only allow 'GET' & 'POST' method to access this view
\@api_view(['GET','POST'])
def api_home(request):
	product=Products.objects.all().order_by('?').first()
	data={}
	if product:
		data=model_to_dict(product,feilds=['id','name'])
	return Response(data)
```

**Make shure that you have included 'rest_framework' in your setting.py under INSTALLED_APPS**


