# Migration Guide

*Updated: 2025-10-23*

Migration Guide: Removal of Essential Settings and Configuration
===========================================================

### Introduction

This migration guide is intended to help you navigate the breaking change introduced by the removal of essential settings and configurations from the project. The change affects critical components such as database connections, user authentication, and template rendering.

### What Changed and Why

The essential settings and configurations, including database, authentication, and template settings, have been removed from the project. This change was made to refactor the project's architecture and improve its maintainability. However, this change will break the project's functionality, and a migration is required to restore the project's operability.

### Step-by-Step Migration Instructions

To migrate your project, follow these steps:

1. **Restore Database Settings**:
	* Create a new file named `database_settings.py` in the `CollegeERP` directory.
	* Add the following code to `database_settings.py`:
	```python
# database_settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': 'db.sqlite3',
    }
}
```
	* In `settings.py`, add the following line to import the database settings:
	```python
# settings.py
from .database_settings import DATABASES
```
2. **Restore Authentication Settings**:
	* Create a new file named `authentication_settings.py` in the `CollegeERP` directory.
	* Add the following code to `authentication_settings.py`:
	```python
# authentication_settings.py
AUTHENTICATION_BACKENDS = [
    'django.contrib.auth.backends.ModelBackend',
]

LOGIN_URL = '/login/'
LOGIN_REDIRECT_URL = '/home/'
LOGOUT_URL = '/logout/'
LOGOUT_REDIRECT_URL = '/login/'
```
	* In `settings.py`, add the following lines to import the authentication settings:
	```python
# settings.py
from .authentication_settings import AUTHENTICATION_BACKENDS, LOGIN_URL, LOGIN_REDIRECT_URL, LOGOUT_URL, LOGOUT_REDIRECT_URL
```
3. **Restore Template Settings**:
	* Create a new file named `template_settings.py` in the `CollegeERP` directory.
	* Add the following code to `template_settings.py`:
	```python
# template_settings.py
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],
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
```
	* In `settings.py`, add the following line to import the template settings:
	```python
# settings.py
from .template_settings import TEMPLATES
```
4. **Update API Security Settings**:
	* In `settings.py`, add the following lines to update the API security settings:
	```python
# settings.py
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.BasicAuthentication',
        'rest_framework.authentication.SessionAuthentication',
    ],
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
}
```
5. **Update `urls.py` and `wsgi.py`**:
	* In `urls.py`, add the following lines to update the URL patterns:
	```python
# urls.py
from django.urls import path, include
from . import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include('api.urls')),
    path('', include('app.urls')),
]
```
	* In `wsgi.py`, add the following lines to update the WSGI application:
	```python
# wsgi.py
from django.core.wsgi import get_wsgi_application

application = get_wsgi_application()
```

### Code Examples (Before/After)

**Before (Old Code)**
```python
# settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': 'db.sqlite3',
    }
}

AUTHENTICATION_BACKENDS = [
    'django.contrib.auth.backends.ModelBackend',
]

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],
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
```

**After (New Code)**
```python
# database_settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': 'db.sqlite3',
    }
}

# authentication_settings.py
AUTHENTICATION_BACKENDS = [
    'django.contrib.auth.backends.ModelBackend',
]

# template_settings.py
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],
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

# settings.py
from .database_settings import DATABASES
from .authentication_settings import AUTHENTICATION_BACKENDS
from .template_settings import TEMPLATES

REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.BasicAuthentication',
        'rest_framework.authentication.SessionAuthentication',
    ],
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
}
```

### Common Issues and Solutions

* **Issue:** Database connections are not working after migration.
	+ **Solution:** Check the `database_settings.py` file and ensure that the database settings are correct. Also, make sure that the `DATABASES` setting is imported correctly in `settings.py`.
* **Issue:** Authentication is not working after migration.
	+ **Solution:** Check the `authentication_settings.py` file and ensure that the authentication settings are correct. Also, make sure that the `AUTHENTICATION_BACKENDS` setting is imported correctly in `settings.py`.
* **Issue:** Template rendering is not working after migration.
	+ **Solution:** Check the `template_settings.py` file and ensure that the template settings are correct. Also, make sure that the `TEMPLATES` setting is imported correctly in `settings.py`.

### Rollback Instructions

To rollback the changes, follow these steps:

1. **Revert `database_settings.py`**:
	* Delete the `database_settings.py` file.
	* In `settings.py`, remove the line that imports the `DATABASES` setting from `database_settings.py`.
2. **Revert `authentication_settings.py`**:
	* Delete the `authentication_settings.py` file.
	* In `settings.py`, remove the lines that import the `AUTHENTICATION_BACKENDS` setting from `authentication_settings.py`.
3. **Revert `template_settings.py`**:
	* Delete the `template_settings.py` file.
	* In `settings.py`, remove the line that imports the `TEMPLATES` setting from `template_settings.py`.
4. **Revert `settings.py`**:
	* Remove the `REST_FRAMEWORK` setting.
5. **Revert `urls.py` and `wsgi.py`**:
	* In `urls.py`, remove the lines that update the URL patterns.
	* In `wsgi.py`, remove the lines that update the WSGI application.

Note: Rolling back the changes will restore the original functionality of the project, but it is recommended to migrate to the new architecture to take advantage of the improved maintainability and security features.