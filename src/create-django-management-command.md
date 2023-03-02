# Create Django Management Command

([index](Index.md))

Gettings started with folder structures:

```txt
polls/
    __init__.py
    models.py
    management/
        __init__.py
        commands/
            __init__.py
            _private.py 
            closepoll.py
    tests.py
    views.py
```

- `polls/management/commands/_private.py`: `Not Avalaible` as management command.
- `polls/management/commands/closepoll.py`: `Avalaible` as management command.

**Notabene**: For convention and constatability sake, use `longcommandname.py` instead of `long_command_name.py`

## Command with list as args

```python
# polls/management/commands/closepool.py

from django.core.management.base import BaseCommand, CommandError
from apps.models import Question as Poll

class Command(BaseCommand):
    help = 'Closes the specified poll for voting'

    def add_arguments(self, parser):
        parser.add_argument(
            'poll_ids',
            nargs='+', # To use as: `1 2 3 4`
            type=int, 
            help='Ids of Poll to be closed' # Optional
        )
    
    def handle(self, *args, **options):
        for pool_id in options['poll_ids']:
            try:
                poll = Pool.objects.get(pk=poll_id)
            except Pool.DoesNotExist:
                raise CommandError(
                    'Pool "%s" does not exist' % poll_id
                )
            poll.opened = False
            poll.save()

        self.stdout.write(self.style.SUCCESS(
            'Successfully closed pool "%s"' % poll_id
        ))
```

```sh
$ python3 manage.py closepool 2 3 4
Successfully closed pool 2
Successfully closed pool 3
Successfully closed pool 4
```

## Command with flag args

```python
# polls/management/commands/closepool.py

from django.core.management.base import BaseCommand, CommandError
from apps.models import Question as Poll

class Command(BaseCommand):
    def add_arguments(self, parser):
        # Positional arguments
        parser.add_argument('poll_ids', nargs='+', type=int)

        # Named (optional) arguments
        parser.add_argument(
            '--delete',
            action='store_true', # To use as flag args
            help='Delete poll instead of closing it',
        )
        
    def handle(self, *args, **options):
        # ...
        if options['delete']:
            poll.delete()
        # ...
```

```sh
$ python3 manage.py closepool 2 3 4 --delete
Successfully closed pool 2
Successfully closed pool 3
Successfully closed pool 4
```

## Command with optional args

```python
# polls/management/commands/createusers.py

from django.contrib.auth.models import User
from django.core.management.base import BaseCommand
from django.utils.crypto import get_random_string

class Command(BaseCommand):
    help = 'Create random users'

    def add_arguments(self, parser):
        parser.add_argument('total', type=int, help='Indicates the number of users to be created')

        # Optional arguments
        parser.add_argument(
            '-p',
            '--prefix',
            type=str,
            help='Define a username prefix',
        )
    
    def handle(self, *args, **options):
        total = options['total']
        prefix = options['prefix']

        for i in range(total):
            if prefix:
                username = '{prefix}_{random_string}'.format(
                    prefix=prefix,
                    random_string=get_random_string()
                )
            else:
                username = get_random_string()
            User.objects.create_user(
                username=username.
                email='',
                password='123'
            )
```

```sh
python3 manage.py createusers 10

# or
python3 manage.py createusers 10 --prefix custom_user

# or

python3 manage.py createusers 10 --p custom_user
```

## Styling

```python
# polls/management/commands/createusers.py

from django.core.management.base import BaseCommand

class Command(BaseCommand):
    def add_arguments(self, parser):
        # ...
    
    def handle(self, *args, **options):
        # ...
        self.stdout.write(self.style.ERROR('error - A major error.'))
        self.stdout.write(self.style.NOTICE('notice - A minor error.'))
        self.stdout.write(self.style.SUCCESS('success - A success.'))
        self.stdout.write(self.style.WARNING('warning - A warning.'))
        # ...
```

## Cron Job

```sh
# example of cron job that launch everyday at 4 a.m.
# work only on linux

# m h dom mon dow command
0 4 * * * /home/mysite/venv/bin/python /home/mysite/mysite/manage.py mycustomcommand
```

**Notabene**: for Linux, use crontab like above.
