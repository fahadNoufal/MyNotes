```python
>>> from django.forms import ModelForm
>>> from myapp.models import Article

# Create the form class.
>>> class ArticleForm(ModelForm):
...     class Meta:
...         model = Article
...         fields = [
					  'pub_date', 'headline', 'content',			
					  ]
			# exclude can be used to exclude a field if using 
			# '__all__'
			exclude=['pup_date']

# Creating a form to add an article.
>>> form = ArticleForm()

# Creating a form to change an existing article.
>>> article = Article.objects.get(pk=1)
>>> form = ArticleForm(instance=article)
>>> 
>>> # to process and save that form :
>>> article=Article.objects.get(id=pk)
>>> if request.method=='POST':
>>> 	form=ArticleForm(request.POST,instance=article)
>>> 	if form.is_valid():
>>> 		form.save()
```



![[Pasted image 20230505162352.png]]


