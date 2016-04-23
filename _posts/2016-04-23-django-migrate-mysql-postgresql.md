---
layout: post
title: Migrate Django application from MySql to PostgreSql
date: 2016-04-23 22:45:42 +0800
categories: django db
---

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
