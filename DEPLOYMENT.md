# Deploying a Django app on heroku

## Outline
- [Deploying a Django app on heroku](#deploying-a-django-app-on-heroku)
  - [Outline](#outline)
  - [Create a new heroku account](#create-a-new-heroku-account)
  - [Installing Dependencies](#installing-dependencies)
  - [Configure `settings.py`](#configure-settingspy)
  - [Add `Procfile` & `.gitlab-ci.yml`](#add-procfile--gitlab-ciyml)
  - [Create new app on heroku](#create-new-app-on-heroku)
  - [Setup Gitlab CI/Pipeline](#setup-gitlab-cipipeline)

Create a new heroku account
---
Quoting from heroku's website: *"Heroku is a platform as a service (PaaS) that enables developers to build, run, and operate applications entirely in the cloud."*. In layman's term, heroku allows you to deploy your web application written in any languages ranging from python to php.

To use heroku, you must first sign up (duh) by visiting this link: https://signup.heroku.com/

Installing Dependencies
---
In order for your Django app to work on a heroku deployment environment, you first need to install the required dependencies as listed below

```bash
$ pip install whitenoise gunicorn dj-database-url psycopg2
```

And as in any web app framework, everytime you add/remove a dependencies, you need to update your package manager. Which in Python's case, the package manager is `pip`, and all the installed packages metadata are being tracked on your `requirements.txt` file.

So, you need to update your requirements.txt (since you just added new packages to your proejct's pip) by running the command below
```bash
$ pip freeze > requirements.txt
```

Trivial:
1. whitenoise
   > whitenoise is a middleware that allows your Django web app to serve its own static files
2. gunicorn
   > gunicorn is a Python WSGI HTTP Server for UNIX (Heroku deployment environment is built upon unix)
3. dj-database-url
   > dj-database-url is a tool that is used to connects your Django app's database to the dictionary from the heroku DATABASE_URL env vars.
4. psycopg2
   > psycopg/psycopg2 is a PostgreSQL adapter for Python

Configure `settings.py`
---
After installing the required packages, you need to "integrate" those packages to your Django project by adding some lines to your `settings.py` file.

You can follow these steps below to configure your `settings.py` file
1. **import os and dj-database-url**
    <br/> add the following lines just below the `from pathlb import Path` line
    ```py
    ...
    from pathlib import Path

    # import os & dj-database-url
    import dj_database_url
    import os
    ...
    ```

2. **edit `ALLOWED_HOSTS`**
    <br/> You can choose your how you would want to set up `ALLOWED_HOST` between the following two. The first option means that you are allowing any network to be your app's host, whilst the later option only specified the necessary options to be allowed as host.

    It is strongly suggested to use the later option on deployment/production for security reasons.
    ```py
    ALLOWED_HOSTS = ['*']
    ```
    ```py
    ALLOWED_HOSTS = ['localhost', '127.0.0.1', 'HEROKU_APP_NAME.herokuapp.com']
    ```

    Note: HEROKU_APP_NAME refers to the name of the app you created on herokuapp.com

3. **add whitenoise setting**
    <br/> add `'whitenoise.middleware.WhiteNoiseMiddleware'` on `MIDDLEWARE` just below the `django.middleware.security.SecurityMiddleware`.
    ```py
    MIDDLEWARE = [
        'django.middleware.security.SecurityMiddleware',
        ...
        # insert whitenoise setting
        'whitenoise.middleware.WhiteNoiseMiddleware',
        ...
        'django.contrib.sessions.middleware.SessionMiddleware',
        'django.middleware.common.CommonMiddleware',
        'django.middleware.csrf.CsrfViewMiddleware',
        'django.contrib.auth.middleware.AuthenticationMiddleware',
        'django.contrib.messages.middleware.MessageMiddleware',
        'django.middleware.clickjacking.XFrameOptionsMiddleware',
    ]
    ```

    Note: It is to be noted that `django.middleware.security.SecurityMiddleware` need to stay on top/index 0 within the `MIDDLEWARE` list

4. **set up production database**
    <br/> Django uses sqlite3 as its default database system, but heroku deployment environment does not support sqlite3. So, in order to have your database works on deployment, you need to make an adjustment about which database to use when on local and on production. This is where psycopg2 and dj-database-url comes into play

    Below your `DATABASES` config on `settings.py`, add the following lines:
    ```py
    ...
    PRODUCTION = os.environ.get('DATABASE_URL') != None
    if PRODUCTION:
        DATABASES['default'] = dj_database_url.config()
    ...
    ```

5. **add `STATIC_ROOT` variable**
    <br/> Add the following line below `STATIC_URL` on the bottom of `settings.py`

    ```py
    STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
    ```

`settings.py` configuration is all done, yours should pretty much look like this:
```py
"""
Django settings for amfm project.

Generated by 'django-admin startproject' using Django 3.1.4.

For more information on this file, see
https://docs.djangoproject.com/en/3.1/topics/settings/

For the full list of settings and their values, see
https://docs.djangoproject.com/en/3.1/ref/settings/
"""

from pathlib import Path

# NEW: import os and dj-database-url
import dj_database_url
import os

# Build paths inside the project like this: BASE_DIR / 'subdir'.
BASE_DIR = Path(__file__).resolve().parent.parent


# Quick-start development settings - unsuitable for production
# See https://docs.djangoproject.com/en/3.1/howto/deployment/checklist/

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = 'ochad#h2^9(t@0t+^+)fhm$!$7jd0kmm8s0q*9ap9hpl0eivv_'

# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True

# EDIT: edit ALLOWED_HOSTS
ALLOWED_HOSTS = ['*']


# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'example',
    'status',
    'biodata'
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    # NEW: add whitenoise setting
    'whitenoise.middleware.WhiteNoiseMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'amfm.urls'

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
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

WSGI_APPLICATION = 'amfm.wsgi.application'


# Database
# https://docs.djangoproject.com/en/3.1/ref/settings/#databases

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# NEW: set up production database
PRODUCTION = os.environ.get('DATABASE_URL') != None
if PRODUCTION:
    DATABASES['default'] = dj_database_url.config()

# Password validation
# https://docs.djangoproject.com/en/3.1/ref/settings/#auth-password-validators

AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]


# Internationalization
# https://docs.djangoproject.com/en/3.1/topics/i18n/

LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'UTC'

USE_I18N = True

USE_L10N = True

USE_TZ = True


# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/3.1/howto/static-files/

STATIC_URL = '/static/'

# NEW: add STATIC_ROOT variable
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
```

Yang barusan ditambah/di-edit ditandai dengan komentar NEW atau EDIT. Kalau sudah sama, kamu bisa proceed ke langkah selanjutnya :D

Add `Procfile` & `.gitlab-ci.yml`
---
Quoting from heroku docs: *"**`Procfile`** is a mechanism for declaring what commands are run by your application’s dynos on the Heroku platform."*. And **`.gitlab-ci-yml`** is a set of commands that will be executed once Gitlab CI is triggered.

Create two new files with the name `Procfile` (yes, only "Procfile", no file extension needed) and `.gitlab-ci.yml`. Make sure that you add those two files on your project's root directory.

Add the following line to your `Procfile`
```Procfile
web: gunicorn amfm.wsgi --log-file -
```
Note: note that amfm on "amfm.wsgi" above is the project name in this example case. So you should adjust it in accordance to your project name.

And then add the following lines to your `.gitlab-ci.yml`
```
stages:
  - deploy

Deployment:
  image: ruby:2.4
  stage: deploy
  before_script:
    - gem install dpl
    - wget -qO- https://cli-assets.heroku.com/install-ubuntu.sh | sh
  script:
    - dpl --provider=heroku --app=$HEROKU_APPNAME --api-key=$HEROKU_APIKEY
    - export HEROKU_API_KEY=$HEROKU_APIKEY
    - heroku run --app $HEROKU_APPNAME python manage.py migrate
  environment:
    name: production
    url: $HEROKU_APP_HOST
```

Create new app on heroku
---
It is assumed that you already have a heroku account. Then proceed to create new app, it's pretty easy and straightforward so I guess you won't be needing any tutorial for this ;)

Setup Gitlab CI/Pipeline
---
Quoting from gitlab docs: *"Pipelines are the top-level component of continuous integration, delivery, and deployment."*. In layman's term, pipeline allows you to automatically update your heroku app everytime you push new updates (of your django app) to gitlab.

In order for your heroku and gitlab to be connected, you need to set up a set of variables. Follow the steps below in order to do so:
1. Go to your gitlab repository. On the sidebar, go to Settings -> CI/CD -> Variables
2. Add exactly three variables, with each specification follows the instruction below
   - Key = HEROKU_APIKEY; Variable = (check on your heroku account settings to get API Key)
   - Key = HEROKU_APPNAME; Variable = YOUR_APP_NAME
   - Key = HEROKU_APP_HOST; Variable = YOUR_APP_NAME.herokuapp.com
**YOUR_APP_NAME**: (the name of your heroku app that you created earlier)

1. Go check your app dashboard on dashboard.heroku.com. There should be a new running process/pipeline. Wait until it's done, and voila! you have successfully deployed your Django application :D