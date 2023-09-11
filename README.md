<h1>How to Configure Django App in Project</h1>

Here's a corrected version of the steps to configure a Django project:

**Step 1: Configure URLs in the Main App**

In the `urls.py` of your main app (usually named something like `main_app` or `project_name`), include the URLs of your other app (`app1.urls`):

```python
from django.urls import path, include

urlpatterns = [
    path('', include('app1.urls')),
    # ... other URL patterns for your main app ...
]
```

**Step 2: Create URLs in the App**

In the `urls.py` file of your app (`app1`), define the URL pattern for the main view:

```python
from django.urls import path
from app1 import views

urlpatterns = [
    path('', views.index, name='index'),
    # ... other URL patterns for your app ...
]
```

**Step 3: Create a View in the App**

In the `views.py` file of your app (`app1`), create a view function:

```python
from django.shortcuts import render

def index(request):
    return render(request, 'index.html')
```

**Step 4: Create a Templates Folder and HTML File**

Create a folder named `templates` in your app's directory, and within it, create an `index.html` file. This is where your HTML code for the `index` view will go.

Your project structure should look like this:

```
your_project/
    app1/
        templates/
            index.html
    ...
```

**Step 5: Configure Settings in the Main Project**

In the `settings.py` file of your main project, make sure to add your app to the `INSTALLED_APPS` list:

```python
INSTALLED_APPS = [
    # ...
    'app1',
    # ... other apps ...
]

# Add the templates directory to the TEMPLATES setting
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
        # ...
    },
]

# Configure STATICFILES_DIRS for static files
STATICFILES_DIRS = [
    BASE_DIR / "static",
]
```

**Step 6: Create a Model and Register it in Admin**

To create a model in your app (`app1`), define it in the `models.py` file. Here's an example:

```python
from django.db import models

class Customer(models.Model):
    first_name = models.CharField(max_length=50)
    last_name = models.CharField(max_length=50)
    email = models.EmailField()

    def __str__(self):
        return f'{self.first_name} {self.last_name}'
```

Then, in the `admin.py` file of your app (`app1`), register the model with the admin site:

```python
from django.contrib import admin
from app1.models import Customer

admin.site.register(Customer)
```

These are the corrected steps to configure a Django project with a basic view and model. Make sure to adjust folder and file names according to your project's structure and requirements.
