---
title: pyload
description: 
published: true
date: 2022-09-18T05:10:23.030Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:10:20.347Z
---

# pyLoad

Output plugin for [pyLoad](http://pyload.net/) download manager.


## Features

* Scan the accepted feeds for urls
* Scan the feed's html page for additional urls
* Check for prefered hoster
* Add found links as package to pyLoad

## Configuration

{{> Includes/PluginInfo }}

**Example:**

```yaml
pyload:
  api: http://localhost:8000/api
  username: <user>
  password: <pwd>
  package: <package>
  package_password: <package_password>
  folder: <folder>
  queue: [yes|no](/yes|no)
  parse_url: [yes|no](/yes|no)
  hoster:
    - List of prefered hoster
  multiple_hoster: [yes|no](/yes|no)
  enabled: [yes|no](/yes|no)
```

Default values for the config elements:
```
pyload:
  api: http://localhost:8000/api
  queue: yes
  parse_url: no
  hoster: ALL
  multiple_hoster: yes
  enabled: yes
```


### API Access

The **api** parameter should be the address of the webinterface followed by "/api", in case the webinterface runs locally on port 8000 the default value will suffice.
Don't forget to set the correct **username** and **password**.

### How to add downloads

You can define the naming format for the packages to be added with every entry by specifying the **package** parameter accordingly. It is [Jinja](https://flexget.com/wiki/Jinja) enabled and, therefore, allows for a dynamic formatting by applying the [entry](https://flexget.com/wiki/Entry)'s field values.
For example, the following will result in packages like "Foobar - S01E05":
```yaml
pyload:
  ...
  package: '{{series_name}} - {{series_id}}'
  ...
```

If no package formatting is defined, Flexget uses the name of the entry.

This is not yet possible for the definition of the **folder** parameter, which can be used to define a certain download folder. When no folder is supplied pyload will choose the folder name (Usually the package name).

The **queue** parameter specifies whether new packages should be queued immediately or added to the collection instead.

### Hosters and URL Parsing
By default this plugin will accept all hoster, if you want to filter prefered ones lookup the names at pyloads [plugin overview](https://github.com/pyload/pyload/wiki/Supported-Hoster) first.
Then simply create a list like this:

```yaml
hoster:
  - YoutubeCom
  - MyvideoDe
```

When a prefered hoster is found only these links will be added, if not remaining hosters gets added.
To only add the first found prefered hoster set **multiple_hoster** to off.

If **queue** is activated downloads will start immediately, otherwise go to collector and wait for user interaction.

When **parse_url** is activated pyload will load the html page at the feed url and check it for additional links. This is useful for hoster who don't include any links in the feed content. This requires that the feed url to link at an article or page related to the entry and **not** on a general page or front page. You should first make sure that this is the case so no wrong links gets added.

### How to add a password to a package
You can define the password for the package send to pyload, this password will be used for extraction.

For example, the following will result in the package password "test123":

```yaml
pyload:
  ...
  package_password: test123
  ...
```

If no password is defined, FlexGet isn't submitting any additional info.