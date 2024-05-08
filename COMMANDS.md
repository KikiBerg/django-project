## INITIATE A DJANGO PROJECT, USEFUL COMMANDS

### Installing packages
- Install the Django Python package: `pip3 install Django~=4.2.1`
- Add it to the requirements.txt file: `pip3 freeze --local > requirements.txt`

---

### Creating a Django project 
- `django-admin startproject my_project .`
- **Don't forget the dot at the end.** The dot specifies the directory location. 
- Migrate changes and keep the database updated, when there are changes in models.py: `python manage.py migrate`
- In my_project/settings.py file, paste the hostname between the square brackets of ALLOWED_HOSTS and save: `ALLOWED_HOSTS = ['8000-kikiberg-djangoproject-6u8655smw96.ws-eu111.gitpod.io']`
- Start the Django server: `python3 manage.py runserver`

---

### Creating a Django app
- `python3 manage.py startapp app_name`
- 
---

### Create Views
- In *app_name/views.py*, **below** `django.shortcuts import render`, type: 
`from django.http import HttpResponse`
- Below the *# Create your views here.* comment, create a Python function named `index`. 
Inside the function, we are returning a simple HTTP response.

---

### Creating URLs
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
- Append `'app_name'`, to the end of the `INSTALLED_APPS` list.
- **Don't forget the comma at the end.**

---

### Testing the app
- Always make sure to always **save all your files** before running the project. You can also take this opportunity to git add, commit and push your work.
- Open a browser window by returning to the terminal tab and running the Django server `python3 manage.py runserver`. Now you can see the text Hello, world! in the browser.

---

### Key files in project folder:
The top level in Django is a project. A project is like a container for everything we want to do. By default, the project contains a settings file and some other administrative files.
- Key files to note are: **manage.py**, **settings.py**, and **urls.py**.

- **manage.py**: this file is in the root directory, above the project folder. It is used to create apps, run our project and perform some database operations.
- **settings.py**: this file contains the project-wide settings, such as installed apps and database connection information, among other things.
- **urls.py**: This file defines how URLs in the Django project map to specific views in the apps. It essentially acts as a routing table, directing users to the appropriate view functions based on the URL they request. The imported views from the apps are responsible for handling user requests and generating the appropriate responses.

---

### Key files in apps folder:
Inside the project, we create apps. An app’s structure is like a Python package with multiple Python modules within a directory. They’re the things that actually do something, such as a blog, a to-do list, or a poll. A project can contain many, many apps. You could do everything you want with just one app, but for maintainability and good design practices, it is better to separate different functionality into different apps.
- Key files to note are: **models.py**, **views.py**.
- **models.py**: our database models are stored here, which define the structure of the database used by our app.
- **views.py**: this file contains the view code for our app. 

---

### Update code for deployment:
- Install a production-ready webserver for Heroku: `pip3 install gunicorn~=20.1`
- Add gunicorn==20.1.0 to the requirements.txt file: `pip3 freeze --local > requirements.txt`
*Note: gunicorn is a production equivalent of the manage.py runserver used in development but with speed and security optimisation.*

- Create a file named **Procfile** at the root directory of the project (same directory as requirements.txt).
*Note: The Procfile has no file extension.*
- In the Procfile, declare this is a web process followed by the command to execute your Django project: `web: gunicorn my_project.wsgi`. *Note: This assumes your project is named my_project.*
- Note the **space** after the colon.

*Note: gunicorn my_project.wsgi is the command heroku will use to start the server. It works similarly to python3 manage.py runserver.*

- Open the my_project/settings.py file and replace DEBUG=True with DEBUG=False
- Also, in settings.py we need to append the Heroku hostname to the ALLOWED_HOSTS list, in addition to the local host: `,'.herokuapp.com'` *Note: Remember the comma and the dot before herokuapp.*
- git add .
- git commit -m "..."
- git push
