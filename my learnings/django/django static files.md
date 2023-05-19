to set the path to static files :
go to settings.py
```python
STATICFILE_DIRS=[
	BASE_DIR / 'static'
]
```

Then create a `static`  folder in the base dir and inside that create subfolders like `images` , `styles`  ,etc .. where you can store images or css fies
 