# Pense-bete pour me souvenir
### il s'agit d'un autre projet que j'ai decidé a pas commit sur github ...

### Views app

```python
from django.shortcuts import render


# Create your views here.
from .models import Book


def books(request):
    all_books = Book.objects.all()
    return render(request, 'book.html', context={'books': all_books})
```

### urls.py created 


```python
from django.urls import path

from .views import books


urlpatterns = [
    path('', books, name='book-page'),

]
```

```python

def books(request):
    all_books = Book.objects.all()
    return render(request, 'book.html', context={'books': all_books}) #pour envoyer les infos dans la pages
```





### Project files
#### settings.py

```python


# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'book',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'Luffy.urls'

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [Path(BASE_DIR, 'Luffy/templates')], #reconnaitre les .html des templates
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]



""" Pour reconnaitre les fichiers css etc """

# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/3.1/howto/static-files/

STATIC_URL = '/static/' 
STATICFILES_DIRS = [
    Path(BASE_DIR, 'Luffy/static'),
    Path(BASE_DIR, 'book/static')
]


```
### urls.py

```python
from django.contrib import admin
from django.urls import path, include
from .views import index


urlpatterns = [
    path('', index, name='home-page'),  
    path('book/', include('book.urls')), #pages book avec includes
    path('admin/', admin.site.urls),
]
```
