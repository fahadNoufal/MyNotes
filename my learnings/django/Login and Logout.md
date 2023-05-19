importing :
```python
from django.contrib.auth import authenticate,login,logout

user=authhenticate(
		request , username=username , password=password
		)
# this will return a user if authenticated or None if not
if user is not None:
	login(request,user)

#to logout , in views.py
def logoutUser(request):
	logout(request)
	return redirect('home')
```

## To restrict the user from entering page

```python
from django.contrib.auth.decorators import login_required

# add @login_required above, like
\@login_required(login_url='login')
def createRoom(request):
	...
```


## change collected form data

```python
from django.contrib.auth.forms import UserCreationForm**
form= UserCreationForm(request.POST)
if form.is_valid():
	user = form.save(commit=False) #this will fetch data from the form and assign it to the user without committing/saving to db
	# from here you can change the data
	user.username=user.username.lower()
	user.save()
	
```