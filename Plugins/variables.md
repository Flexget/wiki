---
title: variables
description: 
published: true
date: 2022-09-18T05:16:37.822Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:16:35.201Z
---

# Variables

This plugin can do value replacement on your config file . While originally intended to strip off passwords, api keys and other sensitive info from the configuration file, it is also useful to just re-use certain values in multiple places in your configuration. Any of the fields from your variables file can be referenced in the config inside the special delimiters `{? ?}`. Jinja is used under the hood, so any valid jinja expressions are allowed inside the delimeters.

### Example
In this sample `config.yml` we configure the plugin to look for config variables in a file named `variables.yml`:

```yaml
variables: variables.yml
templates:
  tell_me:
    notify_xmpp:
      sender: '{? xmpp.usr ?}'
      password: '{? xmpp.pwd ?}'
      recipient: some@recipient.xyz
      title: 'something new: {{ title }}'
tasks:
  test:
    template:
      - tell_me
    trakt_list:
      username: '{? a_long.time_ago ?}'
      password: '{? a_long.in_a_galaxy ?}'
      list: test
      type: movies
```

And this is the `variables.yml` content:

```yaml
xmpp:
  usr: xxx@yyy.zzz
  pwd: mypassword
a_long:
  time_ago: xxx
  in_a_galaxy: yyy
  far:
    far:
      away: zzz
```

So this will be the resulting `config.yml` before executing tasks:

```yaml
variables: variables.yml
templates:
  tell_me:
    notify_xmpp:
      sender: 'xxx@yyy.zzz'
      password: 'mypassword'
      recipient: some@recipient.xyz
      title: 'something new: {{ title }}'
tasks:
  test:
    template:
      - tell_me
    trakt_list:
      username: 'xxx'
      password: 'yyy'
      list: test
      type: movies
```
### Variables within config
Variables can also be defined directly in the config file.
#### Example
```yaml
variables:
  some_folder: /mnt/somewhere
tasks:
  task_a:
    download: "{? some_folder ?}/movies"
```

### Variables from DB
Variables can be also cached to and loaded from DB. If a variables file is referenced from the configuration file, its contents will be cached to DB and will be accessible via the `/variables/` endpoint in the API.

In order to have the config use the variables from the DB instead of the file, use `variables: yes` in the config file instead of the variable file name. Loading variables from DB and not the file is recommended when using the WebUI/API

### Notes
- Key name have limited support for special characters (at least "-" is not working). Stick with letters and underscore.
- The variables file must stay in the same config.yml location.
- Use singles quotes around URLs in your `variables.yml` file.
