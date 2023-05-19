

## Serializer Class

model:
```python
class Snippet(models.Model):
    created = models.DateTimeField(auto_now_add=True)
    title = models.CharField(max_length=100, blank=True, 
		    default='')
    code = models.TextField()
    linenos = models.BooleanField(default=False)

    class Meta:
        ordering = ['created']
```

serializer:
```python
from rest_framework import serializers
from snippets.models import Snippet

class SnippetSerializer(serializers.Serializer):
    id = serializers.IntegerField(read_only=True)
    title = serializers.CharField(
	    required=False, allow_blank=True, max_length=100
	)
    code = serializers.CharField()
    linenos = serializers.BooleanField(required=False)

    def create(self, validated_data):
        """
        Create and return a new `Snippet` instance, given the 
        validated data.
        """
        return Snippet.objects.create(**validated_data)

    def update(self, instance, validated_data):
        """
        Update and return an existing `Snippet` instance, given 
        the validated data.
        """
        instance.title = validated_data.get(
	        'title', instance.title
	    )
        instance.code = validated_data.get('code', instance.code)
        instance.linenos = validated_data.get(
	        'linenos', instance.linenos
	    )
    
        instance.save()
        return instance
```

The first part of the serializer class defines the fields that get serialized/deserialized.

The `create()` and `update()` methods define how fully fledged instances are created or modified when calling `serializer.save()`

A serializer class is very similar to a Django `Form` class, and includes similar validation flags on the various fields, such as `required`, `max_length` and `default`.


# ModelSerializers

Our `SnippetSerializer` class is replicating a lot of information that's also contained in the `Snippet` model.

In the same way that Django provides both `Form` classes and `ModelForm` classes, REST framework includes both `Serializer` classes, and `ModelSerializer` classes.

Let's look at refactoring our serializer using the `ModelSerializer` class.

```python
class SnippetSerializer(serializers.ModelSerializer):
    class Meta:
        model = Snippet
        fields = [
	    'id', 'title', 'code', 'linenos', 'language', 'style'
	    ]
```


Let's see how we can write some API views using our new Serializer class. For the moment we won't use any of REST framework's other features, we'll just write the views as regular Django views.

Edit the `snippets/views.py` file, and add the following:

```python
from django.http import HttpResponse, JsonResponse
from django.views.decorators.csrf import csrf_exempt
from rest_framework.parsers import JSONParser
from snippets.models import Snippet
from snippets.serializers import SnippetSerializer

@csrf_exempt
def snippet_detail(request, pk):
    """
    Retrieve, update or delete a code snippet.
    """
    try:
        snippet = Snippet.objects.get(pk=pk)
    except Snippet.DoesNotExist:
        return HttpResponse(status=404)

    if request.method == 'GET':
        serializer = SnippetSerializer(snippet)
        return JsonResponse(serializer.data)

    elif request.method == 'PUT':
        data = JSONParser().parse(request)
        serializer = SnippetSerializer(snippet, data=data)
        if serializer.is_valid():
            serializer.save()
            return JsonResponse(serializer.data)
        return JsonResponse(serializer.errors, status=400)

    elif request.method == 'DELETE':
        snippet.delete()
        return HttpResponse(status=204)
```

Note that because we want to be able to POST to this view from clients that won't have a CSRF token we need to mark the view as `csrf_exempt`. This isn't something that you'd normally want to do, and REST framework views actually use more sensible behavior than this, but it'll do for our purposes right now.