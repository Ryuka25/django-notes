# Setting Up Signals

([index](Index.md))

<!-- Content Goes here -->
If you plan to use Django signals in your app, import your application's signals module when your application is ready.

```python
# project/my_app/apps.py

from django.apps import AppConfig


class MyAppConfig(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = 'my_app'

    def ready(self):
        import my_app.signals
```

Considering that this is inside your `signals.py`

```python
# project/my_app/signals.py

from django.db.models.signals import post_save
from django.dispatch import receiver

from django.contrib.auth.models import User
from .models import Profile


# Create Profile when user is created
@receiver(post_save, sender=User)
def create_profile(sender, instance, created, **kwargs):
    if created:
        Profile.objects.create(user=instance)


# Save Profile when user is saved
@receiver(post_save, sender=User)
def save_profile(sender, instance, **kwargs):
    if hasattr(instance, "profile"):
        instance.profile.save()

```