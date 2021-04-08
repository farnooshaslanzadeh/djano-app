# Dockerizing a Django App
Django is a python based web framework. In this exercise we will containerize a django app and launch app with docker-compose. Django app uses Postgresql database, so we will launch also a Postgresql container.

## Dockerfile for django app
1. Use `python:3.9-alpine` as base image
2. Set environment variabile `PYTHONUNBUFFERED` to 1
3. COPY `requirements.txt` to the root dir
5. Install following dependencies with apk package manager:
gcc, libc-dev, linux-headers, postgresql-dev, postgresql-client
6. Install python dependencies with `pip install -r /requirements.txt`
7. Create directory /app
8. Copy app/ directory from your host to this directory
9. Change working directory to /app
10. For security reasons, we don't want to run container as root user. 
Create a group and user both called django and set user to django.

## docker-compose.yaml
### postgresql service
Since our application depends on postgres, we need to launch a postgres container:
1. Use `postgres:13-alpine` as base image
2. Use environment variables to set username, password and default database name(to be created). You can find which variables you need fromo dockerhub. You can set their values as you want.
3. To persist database mount a volume to `/var/lib/postgresql/data`
4. Evaluate if you need to expose postgres port
5. Set restart policy to always

### django app service
1. You must build the image with docker-compose
2. Container must be launched with command `python manage.py migrate && python manage.py runserver 0.0.0.0:3003`
3. Expose application's port to host port 8040
4. Set following environment variables to configure database access:
```
DB_HOST=
DB_NAME=
DB_USER=
DB_PASS=
```
5. Set restart policy to always

## After deployment
1. Launch containers with docker-compose. Check from browser if you see Django initial page.
2. If you see Django page correctly, then turn back to the terminal, get inside of the application
container(which docker command do we use to open bash terminal in a container?) and launch
the followin command to creato a superuser for django: `python manage.py createsuperuser`.
Create user `admin` with password `mypassword`.
3. After creating superuser successfully, go to the /admin endpoint on your browser to log in
to Django. Use the username and password for the user you created above.
4. When you login, try to create a user from the menu. If you're connected to database correctly
you must be able to create a new user. Because its going to be saved in database.
