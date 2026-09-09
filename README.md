# Django Sample Project 4

This project demonstrates the creation of a basic Django website using Python, a virtual environment, Django, Visual Studio Code, and GitHub.

The application displays a simple welcome message in the browser.

---

## Project Structure

The project was created with the following structure:

```text
django_sample_project4/
│
├── pr4env/
│   ├── Include/
│   ├── Lib/
│   ├── Scripts/
│   └── pyvenv.cfg
│
└── pr4site/
    ├── manage.py
    │
    ├── pr4site/
    │   ├── __init__.py
    │   ├── asgi.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    │
    └── welcomescreen4/
        ├── migrations/
        │   └── __init__.py
        ├── __init__.py
        ├── admin.py
        ├── apps.py
        ├── models.py
        ├── tests.py
        └── views.py
```

> `pr4env/` is the Python virtual environment. It is used locally but is not uploaded to GitHub because it is included in `.gitignore`.

---

# Step 1: Create the Main Project Folder

Open PowerShell and create the main project folder:

```powershell
mkdir django_sample_project4
```

The folder created is:

```text
django_sample_project4
```

Move into the newly created folder:

```powershell
cd django_sample_project4
```

The terminal location becomes:

```text
PS C:\Users\ASUS\django_sample_project4>
```

---

# Step 2: Create a Python Virtual Environment

Inside the project folder, create a virtual environment:

```powershell
python -m venv pr4env
```

### Explanation

* `python` runs Python.
* `-m venv` tells Python to use its built-in virtual environment module.
* `pr4env` is the name of the virtual environment.

This automatically creates a folder named:

```text
pr4env
```

The automatically generated structure is approximately:

```text
pr4env/
├── Include/
├── Lib/
├── Scripts/
└── pyvenv.cfg
```

These folders and files are created automatically by Python. They do not need to be created manually.

### `Include/`

Contains files used by packages that may require development/build resources.

### `Lib/`

Contains Python libraries and packages installed inside the virtual environment.

### `Scripts/`

Contains executable files and scripts used by the virtual environment.

On Windows, the PowerShell activation script is located here:

```text
pr4env/Scripts/Activate.ps1
```

### `pyvenv.cfg`

Contains configuration information about the virtual environment and the Python installation used to create it.

---

# Step 3: Activate the Virtual Environment

The virtual environment was activated using PowerShell:

```powershell
.\pr4env\Scripts\activate
```

After successful activation, `(pr4env)` appears at the beginning of the terminal prompt:

```text
(pr4env) PS C:\Users\ASUS\django_sample_project4>
```

This indicates that commands such as `pip install` will operate inside the project's virtual environment.

---

# Step 4: Install Django

With the virtual environment activated, Django was installed using:

```powershell
pip install django
```

Django was installed inside the `pr4env` virtual environment.

The Django version used for this project is:

```text
Django 5.2.17
```

---

# Step 5: Create the Django Project

Create the Django project using:

```powershell
django-admin startproject pr4site
```

Here:

* `django-admin` is Django's command-line utility.
* `startproject` creates a new Django project.
* `pr4site` is the name of the project.

This automatically creates:

```text
pr4site/
├── manage.py
└── pr4site/
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

### Important Django Files

#### `manage.py`

Used to perform Django project management tasks from the terminal.

For example:

```powershell
python manage.py runserver
```

#### `settings.py`

Contains the configuration and settings of the Django project.

#### `urls.py`

Contains the URL configuration of the project.

#### `asgi.py`

Provides the ASGI entry point for the project.

#### `wsgi.py`

Provides the WSGI entry point for the project.

#### `__init__.py`

Allows the directory to be treated as a Python package.

---

# Step 6: Move Into the Django Project

Move into the newly created Django project directory:

```powershell
cd pr4site
```

The terminal now shows:

```text
(pr4env) PS C:\Users\ASUS\django_sample_project4\pr4site>
```

From this location, Django management commands can be executed using:

```powershell
python manage.py
```

---

# Step 7: Create the Django Application

Create an application inside the Django project:

```powershell
python manage.py startapp welcomescreen4
```

The application is named:

```text
welcomescreen4
```

Django automatically creates:

```text
welcomescreen4/
├── migrations/
│   └── __init__.py
├── __init__.py
├── admin.py
├── apps.py
├── models.py
├── tests.py
└── views.py
```

### Files inside `welcomescreen4`

#### `admin.py`

Used for configuring the Django administration interface.

#### `apps.py`

Contains the configuration of the Django application.

#### `models.py`

Used to define database models.

No custom model was created in this project at this stage.

#### `tests.py`

Used for writing automated tests.

#### `views.py`

Contains the view functions that handle HTTP requests.

#### `migrations/`

Contains Django database migration files.

At this stage, the directory only contains:

```text
__init__.py
```

because no custom database model has been created.

---

# Step 8: Register `welcomescreen4` in `settings.py`

Open:

```text
pr4site/pr4site/settings.py
```

Find the `INSTALLED_APPS` section.

The application was added to it:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'welcomescreen4',
]
```

The important addition is:

```python
'welcomescreen4',
```

### Why is this required?

It tells Django that `welcomescreen4` is an installed application belonging to this project.

---

# Step 9: Modify `urls.py`

Open:

```text
pr4site/pr4site/urls.py
```

The URL configuration was modified to connect the root URL to the application's `home` view.

The complete file is:

```python
from django.contrib import admin
from django.urls import path
from welcomescreen4 import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.home, name='home'),
]
```

### Explanation

The following line imports the views from the `welcomescreen4` application:

```python
from welcomescreen4 import views
```

The Django admin URL remains:

```python
path('admin/', admin.site.urls),
```

The following line connects the root URL to the `home` view:

```python
path('', views.home, name='home'),
```

The empty string:

```python
''
```

represents the root URL.

Therefore:

```text
http://127.0.0.1:8000/
```

will be handled by:

```python
views.home
```

---

# Step 10: Create the `home` View

Open:

```text
pr4site/welcomescreen4/views.py
```

The following code was added:

```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("Welcome to My Site welcomescreen project 4")
```

### Explanation

First, `HttpResponse` is imported:

```python
from django.http import HttpResponse
```

Then the `home` view function is defined:

```python
def home(request):
```

The `request` parameter represents the HTTP request received by Django.

The view returns:

```python
return HttpResponse("Welcome to My Site welcomescreen project 4")
```

Therefore, the browser receives and displays:

```text
Welcome to My Site welcomescreen project 4
```

---

# Step 11: How the URL and View Connect

The request flows through the project as follows:

```text
Browser
   │
   │ http://127.0.0.1:8000/
   ▼
pr4site/urls.py
   │
   │ path('', views.home, name='home')
   ▼
welcomescreen4/views.py
   │
   │ home(request)
   ▼
HttpResponse
   │
   ▼
Welcome to My Site welcomescreen project 4
```

In simple terms:

1. The browser requests the root URL.
2. Django checks `pr4site/urls.py`.
3. Django finds the URL pattern:

```python
path('', views.home, name='home')
```

4. Django calls the `home()` view.
5. The view returns an `HttpResponse`.
6. The response text is displayed in the browser.

---

# Step 12: Run the Django Development Server

Start the Django development server:

```powershell
python manage.py runserver
```

Django starts a local development server.

The terminal displays a URL similar to:

```text
Starting development server at http://127.0.0.1:8000/
```

The local website is available at:

```text
http://127.0.0.1:8000/
```

---

# Step 13: Open the Website in the Browser

In Visual Studio Code, the local server URL can be opened by holding:

```text
Ctrl
```

and clicking:

```text
http://127.0.0.1:8000/
```

The browser opens the Django website.

The page displays:

```text
Welcome to My Site welcomescreen project 4
```

---

# Step 14: Stop the Development Server

When finished, stop the development server using:

```text
Ctrl + C
```

in the terminal where the server is running.

---

# Final Result

The Django project was successfully created and configured.

The application:

```text
welcomescreen4
```

contains a `home` view that displays:

```text
Welcome to My Site welcomescreen project 4
```

The website runs locally at:

```text
http://127.0.0.1:8000/
```

The completed project has also been pushed to GitHub.
