# Setting up mailhog on MacOS

([index](../Index.md))


- You need to install mailhog from brew: `$ brew install mailhog`
- Then, configure postfix `$ sudo nano /etc/postfix/main.cf`

    ```python
    # /etc/postfix/main.cf

    ...

    # At the end: add the following snipets
    # For MailHog
    myhostname = localhost
    relayhost = [127.0.0.1]:1025
    ```

- Reload postfix: `$ sudo postfix reload`
- Launch mailhog:
    - `$ mailhog` and then browse: <http://localhost:8025>
    - `$ brew services start mailhog` and then browse: <http://localhost:8025>
- Test mail using:
    ```sh
    echo "Hello world" | mail -s "Test email" teste@example.com`
    ```
