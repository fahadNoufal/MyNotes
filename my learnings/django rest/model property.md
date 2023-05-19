In Django, the `@property` decorator is used to define computed properties on model classes.

These computed properties are not stored as fields in the database but are dynamically calculated based on other fields or model attributes.

Here's an example that demonstrates the use of `@property` in Django models:
```python
from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=50)
    last_name = models.CharField(max_length=50)

    @property
    def full_name(self):
        return f"{self.first_name} {self.last_name}"
```

We define a computed property called `full_name` using the `@property` decorator.

Now, let's see how we can use this computed property:
```python
person = Person(first_name='John', last_name='Doe')
print(person.full_name)  # Output: John Doe
```

It's important to note that `@property` is read-only, meaning you can access the computed property but not set its value directly. If you need to set a value, you would typically define a separate setter method or use a different approach.

# Setter method

In Python, the `@property` decorator allows you to define getter methods for computed properties. 

However, if you also want to define a setter method for the property, you need to use the `@property_name.setter` decorator to associate the setter method with the corresponding property.

Here's the naming convention for the setter method:

1.  Computed property: The name of the property in lower case (snake_case).
2.  Setter method: The name of the computed property, followed by `.setter`.

```python
from django.db import models

class Circle(models.Model):
    radius = models.FloatField()

    @property
    def diameter(self):
        return 2 * self.radius
        
    @diameter.setter
    def diameter(self, value):
        self.radius = value / 2
```

In the example, we have a `Circle` model with a `radius` field. We define a computed property `diameter` using the `@property` decorator. 
We also define a setter method for the `diameter` property using the `@diameter.setter` decorator. This allows us to set the `diameter` property, which in turn updates the `radius` field accordingly.

```python
circle = Circle(radius=5)
print(circle.diameter)  # Output: 10

circle.diameter = 14
print(circle.radius)  # Output: 7.0
```