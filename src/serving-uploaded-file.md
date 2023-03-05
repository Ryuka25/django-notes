# Serving Uploaded File

([index](./Index.md))

<!-- Content Goes here -->
Context: You have uploaded a file and you need to serve this, in order that other application/customer can access to it.

At the end, your project should be something like this:

```
projects/
    config/
        ...
        urls.py
        settings.py
        ...
    media/
        default.png
        # your uploaded file is inside this folder
        # you can have nested folder here
```

```python
# project/config/settings.py

import os
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent

...

MEDIA_URL = "/media/"
MEDIA_ROOT = os.path.join(BASE_DIR, "media")

...
```

```python
# project/config/urls.py

...
from django.conf import settings
from django.conf.urls.static import static

...

urls_pattern = [
    # your project urls here...
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)

...
```

To access your uploaded folder use the following urls pattern: `<SERVER_HOST>/media/<PATH_TO_FILE>` (e.g: 'http://127.0.0.1/media/default.png')
