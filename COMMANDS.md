## INITIATE A DJANGO PROJECT, USEFUL COMMANDS

### Installing packages
- Install the Django Python package: `pip3 install Django~=4.2.1`
- Add it to the requirements.txt file: `pip3 freeze --local > requirements.txt`

---

### Creating a Django project 
- `django-admin startproject my_project .`
- Migrate changes and keep the database updated, when there are changes in models.py: `python manage.py migrate`
- In my_project/settings.py file, paste the hostname between the square brackets of ALLOWED_HOSTS and save: `ALLOWED_HOSTS = ['8000-kikiberg-djangoproject-6u8655smw96.ws-eu111.gitpod.io']`
- Start the Django server: `python3 manage.py runserver`

---

### Creating a Django app
- `python3 manage.py startapp app_name`

---

### Create Views
- In *app_name/views.py*, **below** `django.shortcuts import render`, type: 
`from django.http import HttpResponse`
- Below the *# Create your views here.* comment, create a Python function named `index`. 
Inside the function, we are returning a simple HTTP response.

---

### Creating our URLs
- In *my_project/urls.py* import the **include** function by appending it after a comma to the existing *django.urls import.*
- **Below that**, import the views from the app_name app.
`from hello_world import views as index_views`.
Here we are giving the hello_world/views.py file an alias of index_views. In a one-app project, this would not be strictly necessary. However, in a multiple-app project using descriptive alias names makes your urls.py file much easier to read and maintain.
- **Above** the *admin pattern* in *urlpatterns* add:
`path('', index_views.index, name='index'),`

---

### settings.py
- Finally, we just need to add our app to the **settings.py** file to connect the app to the project. For our simple app, this is not strictly necessary, but it's good practice and will be required later on when app models are connecting to databases.
- To connect the app you will need to scroll down through the **my_project/settings.py** file to find the `INSTALLED_APPS` list.
- Append `'hello_world'`, to the end of the `INSTALLED_APPS` list.
- **Don't forget the comma at the end.**

---

### Testing our app
- Always make sure to always **save all your files** before running the project. You can also take this opportunity to git add, commit and push your work.