# Django

## Setting Up a Project

```bash
# start a new Django project
django-admin startproject myproject .

# run db migration
python manage.py migrate

# run the server
python manage.py runserver
```

## Starting an App

A Django project is organized as a group of individual apps that work together to make the project work as a whole.

```bash
# start a new Django app
cd myproject
django-admin startapp myapp
```

### Define Models

Inside `myapp/models.py` ,

```python
from django.db import models


class Topic(models.Model):
    text = models.CharField(max_length=200)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.text


class Entry(models.Model):
    topic = models.ForeignKey(Topic, on_delete=models.CASCADE)
    text = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)

    class Meta:
        verbose_name_plural = "entries"

    def __str__(self):
        return f"{self.text[:50]}..."
```

### Activating Models

To use our models, we have to tell Django to include our app in the overall project. Open `settings.py` (in the myproject directory); you’ll see a section that tells Django which apps are installed in the project:

inside `myproject/settings.py` ,

> It’s important to place your own apps before the default apps, in case you need to override any behavior of the default apps with your own custom behavior.

```python
# ...
INSTALLED_APPS = [
    # My apps
    "myapp",
    # Default Django apps
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
]
```

Whenever we want to modify the data that the app manages, we’ll follow these three steps:

1. modify `models.py`
2. call `makemigrations` on the app: The command `makemigrations` tells Django to figure out how to modify the database so it can store the data associated with any new models we’ve defined.

```bash
python manage.py makemigrations myapp
```

3. tell Django to migrate the project

```bash
python manage.py migrate
```

### The Django Admin Site

```bash
# setting up a superuser
python manage.py createsuperuser
```

now you can access the admin site at `http://127.0.0.1:8000/admin/`

#### Registering a Model with the Admin Site

Inside `myapp/admin.py` ,

```python
from django.contrib import admin
from .models import Topic, Entry

admin.site.register(Topic)
admin.site.register(Entry)
```

## Add Home Page

Making web pages with Django consists of three stages:

1. defining URLs
2. writing views
3. writing templates

Each URL maps to a particular view. The view function retrieves and processes the data needed for that page. The view function often renders the page using a template, which contains the overall structure of the page.

### Mapping a URL

Inside `myproject/urls.py`, which defines URLs for the project as a whole, the `urlpatterns` variable includes sets of URLs from the apps in the project,

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path("admin/", admin.site.urls), # defines all the URLs that can be requested from the admin site
    path("", include("myapp.urls")) # include the URLs for myapp
]
```

Inside `myapp/urls.py`, we declare a list of individual pages that can be requested from "myapp".

The actual URL pattern is a call to the `path()` function, which takes 3 arguments,

1. is a string that helps Django route the current request properly
2. specifies which function to call in `views.py`
3. provides the `name` index for this URL pattern so we can refer to it more easily in other files throughout the project

```python
from django.urls import path
from . import views

app_name = "myapp"
urlpatterns = [
    path("", views.index, name="index") # Home page
]
```

### Writing a View

Inside `myapp/views.py`, a view function takes in information from a request, prepares the data needed to generate a page.

```python
from django.shortcuts import render

def index(request):
    return render(request, "myapp/index.html")
```

### Writing a Template

We can create a base(parent) template that all templates in the project can inherit from.

Inside the template, we use a template tag, which is indicated by braces and percent signs `{% %}`. A template tag generates information to be displayed on a page.

Create `myapp/templates/myapp/base.html` as the parent template,

```htmldjango
<p>
  <a href="{% url 'myapp:index' %}">Learning Log</a>
</p>

{% block content %}{% endblock content %}
```

The template tag `{% url 'myapp:index' %}` shown here generates a URL matching the URL pattern defined in `myapp/urls.py` with the name 'index' . In this example, `myapp` is the namespace and `index` is a uniquely named URL pattern in that namespace. The namespace comes from the value we assigned to 'app_name' in the `myapp/urls.py` file.

On the last line, we insert a pair of block tags. This block, named 'content', is a placeholder; the child template will define the kind of information that goes in the content block.

Create `myapp/templates/myapp/index.html` as the child template,

```htmldjango
{% extends "myapp/base.html" %}

{% block content %}
<p>
  Leanrning log helps you keep track of your learning, for any topic you're
  learning about.
</p>
{% endblock content %}
```

A child template must have an `{% extends %}` tag on the first line to tell Django which parent template to inherit from.

We define the content block by inserting a `{% block %}` tag with the name 'content'. Everything that we aren’t inheriting from the parent template goes inside the content block.

## Add Pages to Display Data

Continue to follow the three steps for adding other two pages:

1. the general topics page: show all topics that users have created
2. the page to display entries for a single topic

First, define URL pattern in `myapp/urls.py`,

```python
urlpatterns = [
    path("", views.index, name="index"),  # Home page
    path("topics/", views.topics, name="topics"),  # Topics page
    path("topics/<int:topic_id>", views.topic, name="topic"), # Topic page
]
```

Second, handle views. The `topics()`, `topic()` functions need to retrieve some data from the database and send it to the template. Here we define a context that we’ll send to the template.

```python
def topics(request):
    topics = Topic.objects.order_by("created_at")
    context = {"topics": topics}
    return render(request, "learning_logs/topics.html", context)

def topic(request, topic_id):
    topic = Topic.objects.get(id=topic_id)
    entries = topic.entry_set.order_by("-created_at")
    context = {"topic": topic, "entries": entries}
    return render(request, "learning_logs/topic.html", context)
```

Lastly, add templates.

Add `myapp/templates/myapp/topics.html`,

```htmldjango
{% extends "learning_logs/base.html" %}

{% block content %}
    <p>Topics</p>
    <ul>
        {% for topic in topics %}
            <li><a href="{% url "learning_logs:topic" topic.id %}">{{topic.text}}</a></li>
        {% empty %}
            <li>No topics!</li>
        {% endfor %}
    </ul>
{% endblock content %}
```

Add `myapp/templates/myapp/topic.html`,

```htmldjango
{% extends "learning_logs/base.html" %}

{% block content %}
    <p>Topic: {{topic.text}}</p>
    <p>Entries:</p>
    <ul>
        {% for entry in entries %}
            <li>
                <p>{{ entry.created_at|date:'M d, Y H:i' }}</p>
                <p>{{ entry.text|linebreaks }}</p>
            </li>
        {% empty %}
            <li>There are no entries for this topic yet.</li>
        {% endfor %}
    </ul>
{% endblock content %}
```

## Allowing Users to Enter Data

The simplest way to build a form in Django is to use a `ModelForm`.

### The Topic ModelForm

```python
from django import forms
from .models import Topic


class TopicForm(forms.ModelForm):
    class Meta:
        model = Topic
        fields = ["text"]
        labels = {"text": ""}
```
