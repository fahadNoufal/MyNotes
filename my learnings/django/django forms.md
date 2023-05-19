Django handles three distinct parts of the work involved in forms:

-   preparing and restructuring data to make it ready for rendering
-   creating HTML forms for the data
-   receiving and processing submitted forms and data from the client
 
It is _possible_ to write code that does all of this manually, but Django can take care of it all for you.

## Django Form class

A form class describes a form and determines how it works and appears.

a form class’s fields map to HTML form `<input>` elements. (A [`ModelForm`](https://docs.djangoproject.com/en/4.1/topics/forms/modelforms/#django.forms.ModelForm "django.forms.ModelForm") maps a model class’s fields to HTML form `<input>` elements via a [`Form`](https://docs.djangoproject.com/en/4.1/ref/forms/api/#django.forms.Form "django.forms.Form"))

 A [`DateField`](https://docs.djangoproject.com/en/4.1/ref/forms/fields/#django.forms.DateField "django.forms.DateField") and a [`FileField`](https://docs.djangoproject.com/en/4.1/ref/forms/fields/#django.forms.FileField "django.forms.FileField") handle very different kinds of data and have to do different things with it.

```python
from django import forms

class NameForm(forms.Form):
	your_name=forms.CharField(
			label='Your name',max_length=100)
```

We’ve applied a human-friendly label to the field, which will appear in the `<label>` when it’s rendered (although in this case, the [`label`](https://docs.djangoproject.com/en/4.1/ref/forms/fields/#django.forms.Field.label "django.forms.Field.label") we specified is actually the same one that would be generated automatically if we had omitted it).

 It puts a `maxlength="100"` on the HTML `<input>`

A [`Form`](https://docs.djangoproject.com/en/4.1/ref/forms/api/#django.forms.Form "django.forms.Form") instance has an [`is_valid()`](https://docs.djangoproject.com/en/4.1/ref/forms/api/#django.forms.Form.is_valid "django.forms.Form.is_valid") method, which runs validation routines for all its fields. When this method is called, if all fields contain valid data, it will:

-   return `True`
-   place the form’s data in its [`cleaned_data`](https://docs.djangoproject.com/en/4.1/ref/forms/api/#django.forms.Form.cleaned_data "django.forms.Form.cleaned_data") attribute.

![[Pasted image 20230505142100.png]]


### The view

Form data sent back to a Django website is processed by a view, generally the same view which published the form. This allows us to reuse some of the same logic.

```python
from django.http import HttpResponseRedirect
from django.shortcuts import render

from .forms import NameForm

def get_name(request):
    # if this is a POST request we need to process the form data
    if request.method == 'POST':
        # create a form instance and populate it with data from the request:
        form = NameForm(request.POST)
        # check whether it's valid:
        if form.is_valid():
            # process the data in form.cleaned_data as required
            # ...
            # redirect to a new URL:
            return HttpResponseRedirect('/thanks/')

    # if a GET (or any other method) we'll create a blank form
    else:
        form = NameForm()

    return render(request, 'name.html', {'form': form})
```

If the form is submitted using a `POST` request, the view will once again create a form instance and populate it with data from the request: `form = NameForm(request.POST)` This is called “binding data to the form” (it is now a _bound_ form).

We call the form’s `is_valid()` method; if it’s not `True`, we go back to the template with the form. This time the form is  populated with the data previously submitted, where it can be edited and corrected as required.

If `is_valid()` is `True`, we’ll now be able to find all the validated form data in its `cleaned_data` attribute. We can use this data to update the database or do other processing before sending an HTTP redirect to the browser telling it where to go next.

### Template
```python
<form action="/your-name/" method="post">
    {% csrf_token %}
    {{ form }}
    <input type="submit" value="Submit">
</form>
```
![[Pasted image 20230505142718.png]]

![[Pasted image 20230505143029.png]]

![[Pasted image 20230505143148.png]]

## Model form

```python
from django.forms import ModelForm
from .models import Room

class RoomForm(ModelForm):
	class Meta:
		model=Room
		field='__all__'
```

