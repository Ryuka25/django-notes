# Crontab

([index](Index.md))

## For MacOs and Linux

- Step 1: Create a `work.sh` for automation process.

```txt
home/
    .scripts/
        work.sh
```

- Step 2: Add new job in crontab. (one line <=> one job)

```sh
crontab -e
```

```txt
# Format of crontab
* * * * * command
* - minute              (0 - 59)
* - hour                (0 - 23)
* - day of the month    (1 - 31)
* - month               (1 - 12)
* - day of the week     (0 - 6, 0 is Sunday)
command - command to execute
```

- Step 3: Save and exit editor. Confirm the new added job.

```sh
crontab -l
```

## For Windows

### Using `Scheduled Tasks` in windows

- Log as administrator
- Start -> Control Panel -> System and Security -> Administrative Tools -> Task Scheduler:
  - Basic Task:
    - Action -> Create Basic Task -> Type a name and Click Next
    - Follow through the wizard
  - Task:
    - Give the Task title
    - Got to actions
    - Go to CMD to find the path to python (use `wich python` in a `Git Bash`) to populate the `Program/script field`
    - Arguments: name of the python script (like run.py)
    - Start in: dir location of python script (like: C:\Users\admin\Documents\my_python_project)
    - Go to Triggers, schedule as you like
    - Test the script by running it

### Using `Windows Subsystem for Linux`

This solution allow to use `crontab` with windows.
