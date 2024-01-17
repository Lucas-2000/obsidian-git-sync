**Vamos criar nosso aplicativo no Django Teste**

Para criar a aplicação no Django rode comando abaixo. “myapp” é nome do seu **Aplicativo**.

```
python manage.py startapp myapp
```

Agora precisamos registrar nossa aplicação no _INSTALLED_APPS_ localizado em _settings.py_.

_myapp_/_templates_/_index.html_

```
{% extends 'base.html' %}
{% block title %}Pagina 1{% endblock %}
{% block content %}
	<h1>Pagina 1</h1>
	<p>Testando o context Global</p>
	<p>{{social}}</p>
{% endblock %}
```

_myapp_/_views.py_

```
from django.shortcuts import render

# Create your views here.
def index(request):
    return render(request, 'index.html')
```

criar arquivo _myapp_/_urls.py_

```
from django.urls import path 
from pages import views

urlpatterns = [
    path('', views.index, name='home'), 
]
```

core/settings.py

```
PROJECT_APPS = [ 
    'apps.pages', 
]
```

urls.py do projeto. _**core/urls.py**_

```
from django.contrib import admin
from django.urls import path, include # adicionar include
from django.conf import settings
from django.conf.urls.static import static 

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('pages.urls')), # url do app
]
urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT) # Adicionar Isto
urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT) # Adicionar Isto
```

Rodar o projeto para ver como está.

```
python manage.py makemigrations
python manage.py migrate
python manage.py runserver
```