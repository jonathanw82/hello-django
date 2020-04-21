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