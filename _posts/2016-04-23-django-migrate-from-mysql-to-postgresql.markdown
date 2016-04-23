---
layout: post
title:  "Migrate django app from mysql to postgresql"
date:   2016-04-23 00:34:12 +0800
categories: jekyll update
---

Today my poor 512M ram digitalocean is running full with hubot and mysql. I hate mysql for so much memory consuming and move to postgresql. Django provide very good abstraction to seperate different layer so that db migration happen so easy. I just wanna try sqllite if postgresql still use too much memory.


#1. config DATABASES in setting.py of django project:
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql', 
            ...
            },
        'postgresql': {
            'ENGINE': 'django.db.backends.postgresql_psycopg2',
            'NAME': 'XXX',
            'USER': 'XXX',
            'PASSWORD': 'XXX',
            'HOST': 'localhost',
            'PORT': '5432',
            }
    }
    
#2. Run makemigrations
    python manage.py makemigrations
> make sure blank=True field should also config as null=True if the field is not populated automatically

#3. Run migrate
    python manage.py migrate --database=postgresql
> --database is use to specify the postgresql db connection to apply

#4. dumping old data
    python manage.py dumpdata --all --natural --indent=4 > dbname.json
> --natural means to use natrual key

> --indent specify the indent format

#5. flush db for existing initial data
    python manage.py sqlflush --database=postgresql

#6. loading data into postgresql
    python manage.py loaddata dbname.json --database=postgresql

#7. change the DATABASES to use postgresql as default
    DATABASES = {
    'mysql': {
        'ENGINE': 'django.db.backends.mysql', 
        ...
        },
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'XXX',
        'USER': 'XXX',
        'PASSWORD': 'XXX',
        'HOST': 'localhost',
        'PORT': '5432',
        }
    }
