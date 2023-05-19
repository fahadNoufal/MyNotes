
In py_client.py (which is sending data to django rest api):
```python
import requests
endpoint = 'http://localhost:8000/api/'
http_response = requests.get(
	endpoint,json={'Title':'Some text'}
)
print(http_response.json())
```

In views:
```python
from .serializers import ProductSerializers
@api_view(['POST'])
def api_home(request):
	data= request.data # this will return the same data send through post method by the client
	serializer = ProductSerializer(data)
	if serializer.is_valid(raise_exception=True):
		#'raise_exception' will give a detailed response if the data is not valid . It wil return a dict with problem when we print serializer.data , like {'title':['This field is required']}
		
		instance = serializer.save() #very similar to form.save()
		print(instance)
		print(serializer.data)
	return Response(serializer.data)
```

1. `data = request.data`: This line assigns the data from the incoming request to the variable `data`. The `request` object likely contains information sent by the client

2. `serializer = ProductSerializer(data)`:  serializer help with data validation, deserialization, and serialization. The `data` argument is passed to the serializer constructor, indicating that the serializer will operate on this data.
   
   Here, a serializer object named `serializer` is created based on a class called `ProductSerializer`.

3. `if serializer.is_valid()` : This condition checks if the data passed to the serializer is valid according to the serializer's defined validation rules and returns true or false.
						