# Crud_Python

- O objetivo deste projeto é demonstrar um projeto de CRUD (Create, Read, Update, Delete). O aplicativo permite que o usuário crie, visualize, atualize e exclua dados de um banco de dados, dentro de um conjunto de páginas web: ("`CRUD em Python`","`Formulário`","`Visualização`").

- O arquivo de execussão é o `main`.

- O output é o site com o CRUD.

- Para a execução do código, escreva, no Terminal: "python manage.py runserver".

## Instalação

- Para executar este projeto, é necessário ter o Python e o Django instalados em seu computador. Você também precisa ter um banco de dados SQLite instalado. Você pode instalar essas dependências seguindo as instruções abaixo:

- Para instalar o Python, acesse o site oficial do Python e faça o download da versão mais recente para o seu sistema operacional: https://www.python.org/downloads/

- Para instalar o SQLite, acesse o site oficial do SQLite e faça o download da versão mais recente para o seu sistema operacional: https://www.sqlite.org/download.html

## Bibliotecas

- Para a intalação do Django, junto as outras bibliotecas necessárias no Terminal, escreva: "`pip install -r requirements.txt`". Isso irá instalar todas as biblíotecas necessárias.

| Command | Description |
| --- | --- |
| pip install -r requirements.txt | Irá instalar todas as biblíotecas necessárias |

## No Django

- Para configurar o Django:

    1 - Crie um novo projeto Django executando o seguinte comando no terminal:

```python
    django-admin startproject project_name
```

- Em `project_name` você insere o nome do projeto.

    2 - Crie um novo aplicativo Django executando o seguinte comando no terminal:

```python
    python manage.py startapp app_name
```

- Em `app_name` você insere o nome do app.

    3 - No arquivo "settings.py" do seu projeto Django, configure o banco de dados SQLite:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```

- Preencha o nome `NAME` do Banco de Dados.

    4 - No arquivo "urls.py" do seu aplicativo Django, configure as rotas para as visualizações CRUD:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('create/', views.create, name='create'),
    path('read/<int:id>/', views.read, name='read'),
    path('update/<int:id>/', views.update, name='update'),
    path('delete/<int:id>/', views.delete, name='delete'),
]
```

- Depois crie as visualizações CRUD no arquivo "views.py" do seu aplicativo Django:

```python
from django.shortcuts import render, redirect
from .models import Item
from .forms import ItemForm

def index(request):
    items = Item.objects.all()
    return render(request, 'index.html', {'items': items})

def create(request):
    form = ItemForm(request.POST or None)
    if form.is_valid():
        form.save()
        return redirect('index')
    return render(request, 'form.html', {'form': form})

def read(request, id):
    item = Item.objects.get(id=id)
    return render(request, 'item.html', {'item': item})

def update(request, id):
    item = Item.objects.get(id=id)
    form = ItemForm(request.POST or None, instance=item)
    if form.is_valid():
        form.save()
        return redirect('index')
    return render(request, 'form.html', {'form': form})

def delete(request, id):
    item = Item.objects.get(id=id)
    if request.method == 'POST':
        item.delete()
        return redirect('index')
```

## Ferramentas

- Foi usado Python como linguagem de programação, o Django como framework web e o SQLite como banco de dados.

### Translated

# Crud_Python
- The purpose of this project is to demonstrate a CRUD (Create, Read, Update, Delete) project. The application allows the user to create, view, update, and delete data from a database within a set of web pages: ("CRUD in Python", "Form", "View").

- The execution file is main.

- The output is the site with the CRUD.

- To the execution, in the terminal, write: "python manage.py runserver".

## Installation

- To run this project, you need to have Python and Django installed on your computer. You also need to have a SQLite database installed. You can install these dependencies by following the instructions below:

- To install Python, go to the official Python website and download the latest version for your operating system: https://www.python.org/downloads/

- To install SQLite, go to the official SQLite website and download the latest version for your operating system: https://www.sqlite.org/download.html

## Libraries

- To install Django, along with other necessary libraries in the Terminal, type: "pip install -r requirements.txt". This will install all the required libraries.
Command	Description
pip install -r requirements.txt	This will install all the required libraries.

- In Django

To set up Django:

1 - Create a new Django project by running the following command in the terminal:

```python
    django-admin startproject project_name
```
- In project_name you insert the name of the project.

2 - Create a new Django application by running the following command in the terminal:

```python
    python manage.py startapp app_name
```

- In app_name you insert the name of the app.

3 - In the "settings.py" file of your Django project, configure the SQLite database:

```python
Copy code
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
Fill in the name NAME of the Database.
```

4 - In the "urls.py" file of your Django application, configure the routes for the CRUD views:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('create/', views.create, name='create'),
    path('read/<int:id>/', views.read, name='read'),
    path('update/<int:id>/', views.update, name='update'),
    path('delete/<int:id>/', views.delete, name='delete'),
]
Then create the CRUD views in the "views.py" file of your Django application:
python
Copy code
from django.shortcuts import render, redirect
from .models import Item
from .forms import ItemForm

def index(request):
    items = Item.objects.all()
    return render(request, 'index.html', {'items': items})

def create(request):
    form = ItemForm(request.POST or None)
    if form.is_valid():
        form.save()
        return redirect('index')
    return render(request, 'form.html', {'form': form})

def read(request, id):
    item = Item.objects.get(id=id)
    return render(request, 'item.html', {'item': item})

def update(request, id):
    item = Item.objects.get(id=id)
    form = ItemForm(request.POST or None, instance=item)
    if form.is_valid():
        form.save()
        return redirect('index')
    return render(request, 'form.html', {'form': form})

def delete(request, id):
    item = Item.objects.get(id=id)
    if request.method == 'POST':
        item.delete()
        return redirect('index')
```