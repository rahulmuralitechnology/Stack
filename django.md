Creating an API for a database using Django can be done in several ways, but one of the most straightforward methods is to use the Django REST framework. Here are the steps to create an API for a database using Django and Django REST framework:

Step 1: Install Django and Django REST framework

If you haven't already done so, you will need to install Django and Django REST framework. You can do this by running the following commands in your terminal:

```
pip install django
pip install djangorestframework
```

Step 2: Create a new Django project

Create a new Django project using the following command:

```
django-admin startproject myproject
```

Step 3: Create a new Django app

Create a new Django app using the following command:

```
python manage.py startapp myapp
```

Step 4: Create a model

In this step, you will create a model for your database. Open the `models.py` file in your app directory (`myapp/models.py`) and define your model. For example:

```python
from django.db import models

class MyModel(models.Model):
    name = models.CharField(max_length=255)
    description = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
```

Step 5: Create a serializer

In this step, you will create a serializer to convert your model instances into JSON format. Open the `serializers.py` file in your app directory (`myapp/serializers.py`) and define your serializer. For example:

```python
from rest_framework import serializers
from myapp.models import MyModel

class MyModelSerializer(serializers.ModelSerializer):
    class Meta:
        model = MyModel
        fields = ['id', 'name', 'description', 'created_at']
```

Step 6: Create a viewset

In this step, you will create a viewset to define the CRUD operations for your API. Open the `views.py` file in your app directory (`myapp/views.py`) and define your viewset. For example:

```python
from rest_framework import viewsets
from myapp.models import MyModel
from myapp.serializers import MyModelSerializer

class MyModelViewSet(viewsets.ModelViewSet):
    queryset = MyModel.objects.all()
    serializer_class = MyModelSerializer
```

Step 7: Define URLs

In this step, you will define the URLs for your API. Open the `urls.py` file in your app directory (`myapp/urls.py`) and define your URLs. For example:

```python
from django.urls import include, path
from rest_framework import routers
from myapp.views import MyModelViewSet

router = routers.DefaultRouter()
router.register(r'mymodels', MyModelViewSet)

urlpatterns = [
    path('', include(router.urls)),
]
```

Step 8: Run the server

In this step, you can run the development server to test your API. Run the following command:

```
python manage.py runserver
```

Step 9: Test the API

You can now test your API by sending requests to the URLs you defined. For example, if you want to get a list of all `MyModel` instances, you can send a GET request to `http://localhost:8000/mymodels/`.

Congratulations, you have now created a RESTful API for your database using Django and Django REST framework!