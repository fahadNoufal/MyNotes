![[Pasted image 20230505124039.png]]

in views.py
```python
from .models import Room
from django.db.models import Q  #search union or intersection

def home(request):
	rooms=Room.objects.all()
	# or
	q=request.GET.get('q')
	rooms = Room.objects.filter(topic__name__icontains=q)
	# icontains returns all which contains any letters of the query without case sensitivity
	# other one is __contains
	rooms=Room.objects.filter(
		Q(topic__name__icontais=q) |
		Q(name__icontains=q) |
		Q(description__icontains=q)
	)

	room_count=rooms.count() #gives the no of rooms

```

## Querying to child objects
```python
def room(request,pk):
	room=Room.objects.get(id=pk)
	messages=room.message_set.all()
	#we can query child objects of a specific model
	# where message is a child model (many to one)
	# also
	messages=room.message_set.all().order_by('-created')

	if request.method=='POST':
		message=Message.objects.create(
			user=request.user,
			room=room,
			body=request.POST.get('body')
		)
		return redirect('room',pk=room.id)

```

