Sight packages to find it = cd /workspace/.pip-modules/lib/python3.7/site-packages/ 
to list out all fiels and directorys = ls -la
to get back to the last directory = cd -
To start a django project = django-admin startproject django_todo .
    the dot at the end means it makes the project in the current directory.

To run the project = python3 manage.py runserver

1. create an app = python3 manage.py startapp todo

2. in views.py define a function called say_hello

3. in urls put from todo.views import say_hello

4. The the path function it takes 3 arguements = path('hello/', say_hello, name='hello')

5. To run the project = python3 manage.py runserver

6. Add a templates folder to to the todo folder

7. In that create a folder called todo

8. In the folder add a file todo_list.html and populate with html

9. change the urls

10. change in views.py

11. In setting.py in the installed apps add todo

Mirgations are djangos way of converting python code to database operations so no need to write any sql code.

Commands we need to know!

1. python3 manage.py makemigrations --dry-run = will run the command so you can see what it would do it we acutally ran it.

2. python3 manage.py showmigrations = make any migrations that need to be applied are applied.

3. python3 manage.py migrate -- plan = the plan flage shows you what its doing to do. 

4. python3 manage.py migrate = will take care of all the migrations.

5. python3 manage.py createsuperuser = it will ask for a username, email and password

6. run the app and go to / admin to login

Now to models.py

create a class item() for entries in the database Model
and migrate them

in admin.py = from .models import Item
Then register the item = admin.site.register(Item)


TESTING:

to run tests = python3 manage.py test

to be more specific of what we are testing = python3 manage.py test todo.test_forms
a specific class of tests = python3 manage.py test todo.test_forms.TestItemForm
or = python3 manage.py test todo.test_forms.TestItemForm.test_fields_are_explicit_in_form_metaclass

COVERAGE:
pip3 install coverage

to run it = coverage run --source=todo manage.py test
then = coverage report
to get a html report = coverage html
to view it = python3 -m http.server

Deployment 

sql lite database can note be used as it gets lost every time it restarts to so we need to install Psycopg2
pip3 install psycopg2-binary

We also need a package called unicorn or green unicorn whitch will replace our deployment server when the app is deployed to heroku.
It will act as our webserver = pip3 install unicorn

make requirments = pip3 freeze --local > requirements.txt

To create a heroku app = heroku apps:create jonathanw82-django-todo-app --region eu

type heroku app to see list of apps = heroku apps

Set up the Postgres as the database go to heroku in resources seatch postgres 
select HobbyDev-free
In config vars a new link to a database we can use will be available

You can see it if you go to = heroku addons

If you wanted to user this with myqsl you can use add on called clearDB instead the steps are the same.

We need to install another package to connect to the remote database called djdburl = pip3 install dj_database_url

To get the URL of the remote database = heroku config
to show the database link urls

in setting.py go to databases and change the default to =  'default': dj_database_url.parse()
and add the link to the db urls

then at the top of settings.py import it with = import os and import dh_database_url

then = python3 manage.py migrate 

create .gitignore and add = *.sqlite3 and __pycashe__/

push to git hub

push to heroku = git push heroku master

an error will happen Error while running '$ python manage.py collectstatic --noinput'.
this is telling us heroku cant find any static files such as javascript or css

to disable this  = heroku config:set DISABLE_COLLECTSTATIC=1
then repush to heroku

we will get another error is we try to run the app so = heroku logs --tail
will let us see the logs error code H14 no web process running

We need to now create a Procfile in the root to tell heroku that we want this to be a web application unicorn with a web server
but we have not told unicorn to start yet in the Procfile put  = web: gunicorn django_todo.wsgi:application 

in settings we have to add ALLOWED_HOSTS = ['jonathanw82-django-todo-app.herokuapp.com']
so heroku trusts this host