---
title: irc
description: 
published: true
date: 2023-01-21T20:36:46.331Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:24:15.663Z
---

# [Daemon](/Daemon) > IRC

This plugin will allow you to connect a bot to an IRC channel. It listens for release announcements, parses them and sends them to the FlexGet daemon, which executes a task of your choice with the input from IRC.

The benefit to this plugin over regular search plugins that utilize API/scraping is that any new downloads will be picked up as soon as they are available.

You can always get the current status of the IRC plugin, as well as restart and stop it, via the [command line](/CLI/irc).

### Prerequisites
* **Install `irc_bot`**.

This plugin requires you to install [the `irc_bot` Python module](https://github.com/cvium/irc_bot) separately. To install, run:

```bash
$ pip install irc_bot
```
  
* Run FlexGet in `daemon` mode. This means you may want to migrate your cron jobs to use the [scheduler plugin](/Plugins/Daemon/scheduler) instead.

```bash
$ flexget daemon start --daemonize
```

* Have an autodl-tracker file relevant to your intended tracker. Either the name (case insensitive) or downloaded from [here](https://github.com/autodl-community/autodl-trackers).
* rsskey or other needed credentials located in the tracker file and in the guide section of your tracker's website. (hint: look for autodl guides)

### Daemon plugin

Note that this is a daemon plugin. Unlike most plugins, it is not placed under the tasks section of the config, but rather is a [top-level key](/Configuration#top-level-keys). Example:

```text
irc:
  my_irc_name:
    <irc_config>
tasks:
  my_task:
    <task_config>
templates:
  my_template:
    <template_config>
```


### Tips

* Read your tracker's wiki/FAQ very carefully. Using this plugin and getting banned for not following rules is your own fault.
* The tasks you use for IRC should have `manual: yes` in them to avoid the scheduler automatically executing them.
* The plugin populates a few IRC-specific entry fields. These are all prefixed with `irc_`. You can see which fields are available by opening the `.tracker` file (see above where to get it). Any lines with the format `<var name="category"/>` will be available, though some of them may be optional.
* When posting logs of this plugin anywhere, make sure your personal information is scrubbed. If you leak your own rsskey etc. you will have to generate a new one or risk getting your account hijacked.
* **We cannot assist you with tracker specific problems unless it's because of a bug in our implementation.**
* Passkey, rsskey, user, uid and the fields you need to specify all vary depending on the tracker. In the `.tracker` file they will most likely be in the `<settings></settings>` block.
* It is _technically_ possible to run this without a tracker file, but then you'd lose the `irc_` prefixed fields. If the message is more than an URL, be prepared to use the manipulate plugin.
* Visit our [Gitter](https://gitter.im/Flexget/Flexget) if you have questions/issues.

### Settings
|  Option  |  Description  | Example |
| --- | --- | --- |
| **tracker_file** |  *(required & preferred, unless **server** & **channels** are specified)* Path to the tracker file for your tracker  |  'MyFunTracker.tracker'  |
| **task** |  *(required: task or task_re)* Task(s) to execute and send entry to  | get_entry  |
| **task_re** |  *(required: task or task_re)* Execute task(s) if all of their defined regex patterns match.  Useful for filtering announcements  |  *see below*  |
| **nickname** |  *(required)* Specify your nickname. Make sure it's allowed.  | myusername-bot  |
| **server** |  Explicitly specify server address  |  irc.someplace.net  |
| **port** |  *(required)* Explicitly specify port number (integer)  |  6667 *(default)*  |
| **password** |  Specify password for server  |  |
| **use_ssl** |  Use SSL when connecting to the server(s).  |  No *(default)*  |
| **channels** |  Explicitly specify announce channel(s). **Joining channels that are not announce-channels can get you banned.** <br><br>Optionally, provide a channel `key` (password) next to the channel name, separated by a space (as of `irc_bot` v1.0.41) | ['#announce_channel'] <br>or<br> ['#channel YourKey'] |
| **nickserv_password** |  Password for authenticating your nickname to nickserv  |   |
| **invite_nickname** |  Some channels require this for authentication  |   |
| **invite_message** |  Some channels require this for authentication  |   |
| **queue_size** |  If set to higher than 1, it will wait until it has received `queue_size` announcements before sending them to the task(s).  |  1 *(default)*  |
| **task_delay** |  The amount of time in seconds to delay task execution. Useful for when announcements are too early (unregistered torrent error).  |  30 |


### task vs task_re
The `task_re` option allows you to specify where to send certain entries eg. send TV announcements to a TV task and movie announcements to a movie task. Any entry field created from the IRC announcement can be used for filtering. The most commonly used is `irc_category`, but you are free to filter on uploader, size or whatever else information is available.

When executing a task using the `task_re` option with multiple patterns defined, the task will only be executed if all of the patterns are a match (an AND condition).  If you have multiple patterns that should execute a task when ANY of them are a match (an OR condition), you can use the same task name with different patterns.

`task` is simpler and will send all entries to the task(s). The filtering will have to be done in the tasks. If your tracker is specialized (e.g. exclusively TV), then `task_re` might be overkill.

The categories are different for each tracker (and may not even called `irc_category`; check the tracker file), but usually they match the category names on their website. You could also just monitor the announcements made in their IRC to understand the pattern.



### Example config
```yaml
irc:
  irc_cool_tracker:
    tracker_file: 'MyFunTracker.tracker'
    nickname: 'flexget_bot' #make sure to check naming conventions before joining
    nickserv_password: '{? irc.nickserv_password ?}'
    port: 7011
    rsskey: '{? irc.rsskey ?}'
    task: get_entry
    channels: ["#myannounces"]
  irc_some_other_tracker:
    tracker_file: 'MyOtherFunTracker.tracker'
    nickname: 'flexget-bot'
    nickserv_password: '{? other_irc.nickserv_password ?}'
    passkey: '{? other_irc.passkey ?}'
    task_re:
      - task: get_movie_entry
        patterns:
          - regexp: Movie
            field: irc_category
          - regexp: 'true'
            field: irc_scene
      - task: get_movie_entry
        patterns:
          - regexp: MovieHD
            field: irc_category
      - task: get_tv_entry_with_tracking
        patterns:
          - regexp: (TV\/x265)|(TV\/x264)|(TV\/Web-DL)
            field: irc_category
    channels: ["#myotherannounce"]    

tasks:
  get_entry:  # this task greedily accepts anything matching the categories
    manual: yes
    if:
      - irc_category in ['Movies', 'TV/HD', 'TV/SD']: accept
    template: download-it

  get_tv_entry_with_tracking:
    metainfo_series: yes
    template: download-it
    trakt_lookup:
      account: '{? trakt.usr ?}'
    if:
      - trakt_watched: reject
    manual: yes
    metainfo_series: yes
    thetvdb_lookup: yes
    configure_series:
      from:
        trakt_list:
          account: '{? trakt.usr ?}'
          list: '{? trakt.tv ?}'
          type: shows
      settings:
        identified_by: ep
        qualities: 
          - 720p hdtv
          - 1080p hdtv
        upgrade: yes
  
  get_movie_entry:
    manual: yes
    template: download-it
    quality: 1080p dvdrip+
    list_match:
      from:
        - movie_list: watchlist
    list_remove:
      - trakt_list:
          account: '{? trakt.usr ?}'
          list: watchlist
    imdb_lookup: yes
    imdb_required: yes
    seen_movies: strict
    proper_movies: yes
    if:
      - trakt_collected: reject
```