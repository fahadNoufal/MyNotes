### Why use serializers ?

normally if we create a model like:
```python
class Products(models.Model):
	name=models.CharField(max_length=100)
	description=models.TextField(blank=True,null=True)
	price=models.DecimalField(
		max_digits=10,decimal_places=2,default=99.99
	)
	@property
	def sale_price(self):
		return "%.2f" %(float(self.price)*0.8)
	def get_discount(self):
		return 'no discount'
```
and in views.py we do this:
```python
@api_view(['GET','POST'])
def api_home(request):
	product=Products.objects.all().order_by('?').first()
	data={}
	if product:
		data=model_to_dict(product,fields=[
			'id','name','sale_price'
		])
	return Response(data)
```

we wont get `sale_price` in response
to get @property 's  we must use `serializers`

### How to use

serializers is made similar to a form
like forms.py create a file serializers.py in your app folder

in serializers.py
```python
from rest_framework import serializers
from .models import Products

class ProductSerializers(serializers.ModelSerializers):
	# to use other key name for a field in a model other than the name specified when creating the model, like 'get_descount' in this case
	# here we are tryna change 'get_descount' to 'my_discount' when accessing through rest_framework api
	my_discount=serializers.SerializerMethodField(
		read_only=True
	)
	class Meta:
		model=Products
		fields=[
			'name',
			'price',
			'sale_price',
			'my_discount'
		]
	# by convension you should use 'get_<var_name>' , here the var is 'my_discount' ,hence function is 'get_my_discount'.
	def get_my_discount(self,obj):
		return obj.get_discount()
	#here the obj is the model object passed in by the queryset , ie, ProductSerializers(instance) => instance model obj
```

and in views:
```python
from .serializers import ProductSerializers
@api_view(['GET','POST'])
def api_home(request):
	instanc=Products.objects.all().order_by('?').first()
	data={}
	if instanc:
		
		data= ProductSerializers(instanc).data
		# returns the dict of instance
	return Response(data)

# if there are many product model to serialize, then :
# instanc=Products.objects.all()
# data= ProductSerializers(instanc,many=True).data
```

Thus we we wil get the reponse data as:
