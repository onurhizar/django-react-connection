# 1) create project root folder
`mkdir fullstackproject`
`cd fullstackproject`


# 2) Pipenv & Django setup
`pipenv shell`
`pipenv install django djangorestframework`


# 3) Create Django project and api app
`django-admin startproject backend .`
`./manage.py startapp api`
`./manage.py migrate`

append INSTALLED_APPS @ backend/settings.py
'rest_framework',
'api',



# 4) Create React app
`npx create-react-app frontend`
`rm -rf .git && rm .gitignore` remove git repo because we will create for whole project


❯ tree -L 2
```
.
├── backend
│   ├── asgi.py
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── frontend
│   ├── node_modules
│   ├── package.json
│   ├── package-lock.json
│   ├── public
│   ├── README.md
│   └── src
├── logs.txt
├── manage.py
├── Pipfile
└── Pipfile.lock
```


# 5) Create react build folder
`cd frontend`
`npm run build`


# 6) Django TEMPLATES Settings @ backend/settings.py (line 61)
change `'DIRS': [],` to
`'DIRS': [BASE_DIR / 'frontend'],`

# 7) Serve React built html file in Django
Create a view for index @ api/views.py
`def indexView(request): return render(request, 'build/index.html')`

@ backend/urls.py
```
from api import views

urlpatterns = [
    path('', views.indexView),
```

# Also setup the static files to serve js/css etc 
add this to backend/settings.py (line 123)
```
STATICFILES_DIRS = [
    BASE_DIR / "frontend" / "build" / "static",
]
```