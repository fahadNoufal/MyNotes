	Clearly, the power of relational databases lies in relating tables to each other.

Django offers ways to define the three most common types of database relationships:
`many-to-one, many-to-many and one-to-one.

## Many-to-one relationships

![[Pasted image 20230505120532.png]]

```python
class Message(models.Model):
	room=models.ForeignKey(Room,on_delete=models.CASCADE)
```


## Many-to-many relationships

![[Pasted image 20230505120759.png]]

It doesn’t matter which model has the [`ManyToManyField`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.ManyToManyField "django.db.models.ManyToManyField"), but you should only put it in one of the models – not both.

Generally, [`ManyToManyField`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.ManyToManyField "django.db.models.ManyToManyField") instances should go in the object that’s going to be edited on a form. 

In the above example, `toppings` is in `Pizza` (rather than `Topping` having a `pizzas` [`ManyToManyField`](https://docs.djangoproject.com/en/4.1/ref/models/fields/#django.db.models.ManyToManyField "django.db.models.ManyToManyField") ) because it’s more natural to think about a pizza having toppings than a topping being on multiple pizzas. The way it’s set up above, the `Pizza` form would let users select the toppings.

## One-to-one relationships

![[Pasted image 20230505121329.png]]

![[Pasted image 20230505121301.png]]


