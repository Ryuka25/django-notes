# Unable to import psycopg2

I was unable to `import psycopg2` on **MacOs High-Sierra (10.13)**

```python
>>> import psycopg2

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/Users/ryuka/***/.venv/lib/python3.7/site-packages/psycopg2/__init__.py", line 51, in <module>
    from psycopg2._psycopg import (                     # noqa
ImportError: dlopen(/Users/ryuka/***/.venv/lib/python3.7/site-packages/psycopg2/_psycopg.cpython-37m-darwin.so, 2): Symbol not found: ____chkstk_darwin
  Referenced from: /Users/ryuka/***/.venv/lib/python3.7/site-packages/psycopg2/.dylibs/libcrypto.1.1.dylib (which was built for Mac OS X 11.0)
  Expected in: /usr/lib/libSystem.B.dylib
 in /Users/ryuka/***/.venv/lib/python3.7/site-packages/psycopg2/.dylibs/libcrypto.1.1.dylib
>>>
```

## Solution

```sh
$ pip install pscyopg2-binary==2.8.6

Collecting psycopg2-binary==2.8.6
  Using cached psycopg2_binary-2.8.6-cp37-cp37m-macosx_10_6_intel.macosx_10_9_intel.macosx_10_9_x86_64.macosx_10_10_intel.macosx_10_10_x86_64.whl (1.5 MB)
Installing collected packages: psycopg2-binary
Successfully installed psycopg2-binary-2.8.6
```

```python
>>> import psycopg2
>>> # psycopg2 imported successfully
```
