# my-own-django-docker-template
Created my own Dockerized Django, DRF, PostgreSQL and Pytest Template for both environments (development and also production) without the need of reconfiguration


How to run this

- 0- Ignore/delete its repo django-project and follow the instructions below to build your own using docker and docker-compose with postgres and pytest!

- 1- Build:
    $ sudo docker-compose build 

- 2- Create a django project (startproject):
    $ sudo docker-compose run --rm quizproject sh -c "django-admin startproject quizproject ."

- 3- Add the Database on settings.py and uncomment it on docker-compose.yml

- 4- Build (Again):
    $ sudo docker-compose build

- 5- Create the app then the model (if needed) to test it up
    $ sudo docker-compose run --rm quizproject sh -c "python manage.py startapp quizapp"

- 6- sudo docker-compose up

- 7- Must work on localhost now 

- just in case keep this from your own generated project: SECRET_KEY = django-insecure-4qiy1z7n&r&s&*czhqpb3mw_($gijq9imi%yqo@f%)36g*-zb5'


### After testing the project on your web browser to see if it's really working, copy the settings,py configurations below and paste it accordingly

- django project settings.py you will need to copy and paste after on your own django project:

**

# From here (start of settings.py)
import os
from pathlib import Path

# Build paths inside the project like this: BASE_DIR / 'subdir'.
BASE_DIR = Path(__file__).resolve().parent.parent

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = os.environ.get('SECRET_KEY')

# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = bool(int(os.environ.get('DEBUG', 0)))

ALLOWED_HOSTS = []
ALLOWED_HOSTS.extend(
    filter(
        None,
        os.environ.get('ALLOWED_HOSTS', '0.0.0.0','').split(','),
    )
)

...
...
...

# At the very bottom of the settings.py paste this below:
STATIC_URL = '/static/'
STATIC_ROOT =  os.path.join(BASE_DIR, 'staticfiles')
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

# To here (end of settings.py)

**