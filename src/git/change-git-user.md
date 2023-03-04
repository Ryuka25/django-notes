# Change Git User

([index](../Index.md))

For a particular project, you need to switch to a specific git project in your personnal desktop or work desktop

## Show a list of git config

```sh
git config -l # include all configuration list
git config -l --local   # repository configuration
git config -l --global  # global configuration
```

- Example for global git user in work machine:

```
$ git config -l --global
user.email=lovanirina.randrianasolo@work.domain
user.name=Lovanirina R
```

- Example of one time git user in work machine for a specific repository:

```
$ git config -l --local
user.email=lovanirina.randrianasolo@personnal.domain
user.name=Lovanirina R.
```

## Change globally

```sh
git config --global user.email "<mail.used.generally.on.machine@exemple.com>"
git config --global user.name "<username.with.mail>"
```

## Change for a particular project

```
git config user.email "<one.time.mail@exemple.com>"
git config user.name "<username.with.mail>"
```
