# Database configuration

([index](./Index.md))

This is how to setup database in django,

## SQLite3


```python
# config/settings.py

...
import os
from pathlib import Path

# Build paths inside the project like this: BASE_DIR / 'subdir'.
BASE_DIR = Path(__file__).resolve().parent.parent

...

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}

...

```

## MySQL

```sh
pip install PyMYSQL
```

```python
# config/settings.py

...

# To work with MySQL Database
import pymysql

pymysql.install_as_MySQLdb()

...

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': '<DB_NAME>',
        'USER': '<DB_USER>',
        'PASSWORD': '<DB_PWD>',
    }
}

...

```

## PostgreSQL

```sh
pip install psycopg2-binary==2.8.6
```

```python
# config/settings.py

...

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': '<DB_NAME>',
        'USER': '<DB_USER',
        'PASSWORD': '<DB_PWD>',
        'HOST': '<DB_HOST>',
        'PORT': <DB_PORT>,
    }
}

...

```
