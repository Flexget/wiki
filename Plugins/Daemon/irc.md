## IRC
<div class="alert alert-info" role="alert">
  <span class="glyphicon glyphicon glyphicon-download-alt"></span>
  &nbsp;
This plugin requires the irc_bot Python module. To install the Python module run: <br/><br/>

```
$ pip install irc_bot
```
</div>

This plugin will allow you to connect a bot to an IRC channel. It listens for release announcements, parses them and sends them to the FlexGet daemon, which executes a task of your choosing with the input from IRC.

The benefit to this plugin over regular search plugins that utilize API/scraping is that any new downloads will be picked up as soon as they are available.

You can alwas get the current status of the IRC plugin via the [commandline](/CLI/irc) as well as restart and stop it.

### Prerequisites
* **Install irc_bot**
* Run Flexget in daemon-mode. (ex: *flexget daemon start --daemonize*). This means you may want to migrate your cron-jobs to use the scheduler plugin instead.
* Have an autodl-tracker file relevant to your intended tracker. Either the name (case insensitive) or downloaded from [here](https://github.com/autodl-community/autodl-trackers).
* rsskey or other needed credentials located in the tracker file and in the guide sections in your tracker website. (hint: look for autodl guides)

### Tips
* **Note that this is a daemon plugin, which unlike a "regular" plugin is not placed under the tasks section of the config, but rather on the root level. Eg.:**

```
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
* Read your tracker's wiki/FAQ very carefully. Using this plugin and getting banned for not following rules is your own fault.
* The tasks you use for irc should have `manual: yes` to avoid the scheduler automatically executing them.
* The plugin populates a few irc-specific Entry fields. They are all prefixed with `irc_`. You can see which fields are available by opening the `.tracker` file (see above where to get it). Any lines with the format `<var name="category"/>` will be available (some of them might be optional though) eg. `irc_category`.
* When posting logs of this plugin anywhere, make sure your personal information is scrubbed. If you leak your own rsskey etc. you will have to generate a new one or risk getting your account hijacked.
* **We cannot assist you with tracker specific problems unless it's because of a bug in our implementation.**
* Passkey, rsskey, user, uid, the fields you need to specify all vary depending on the tracker. In the `.tracker` file they will most likely be in the `<settings></settings>` block.
* It is _technically_ possible to run this without a tracker file, but then you'd lose the irc_ prefixed fields. If the message is more than an URL, be prepared to use the manipulate plugin.
* Visit our [Gitter](https://gitter.im/Flexget/Flexget) if you have questions/issues.

### Settings
|  Option  |  Description  | Example |
| --- | --- | --- |
| **tracker_file** |  *(required & preferred, unless **server** & **channels** are specified)* Path to the tracker file for your tracker  |  'MyFunTracker.tracker'  |
| **task** |  *(required: task or task_re)* Task(s) to execute and send entry to  | get_entry  |
| **task_re** |  *(required: task or task_re)* Execute task(s) if the regex matches the specified field. Useful for filtering announcements  |  *see below*  |
| **nickname** |  *(required)* Specify your nickname. Make sure it's allowed.  | myusername-bot  |
| **server** |  Explicitly specify server address  |  irc.someplace.net  |
| **port** |  (required) Explicitly specify port number (integer)  |  6667 *(default)*  |
| **channels** |  Explicitly specify announce channel(s). **Joining channels that are not announce-channels can get you banned.**  | ['#announce_channel']  |
| **nickserv_password** |  Password for authenticating your nickname to nickserv  |   |
| **invite_nickname** |  Some trackers require this for authentication  |   |
| **invite_message** |  Some trackers require this for authentication  |   |
| **queue_size** |  If set to higher than 1, it will wait until it has received `queue_size` announcements before sending them to the task(s).  |  1 *(default)*  |
| **use_ssl** |  Use SSL when connecting to the server(s).  |  No *(default)*  |
| **task_delay** |  The amount of time in seconds to delay task execution. Useful for when announcements are too early (unregistered torrent error).  |  30 |


### task vs task_re
The `task_re` option allows you to specify where to send certain entries eg. send TV announcements to a TV task and movie announcements to a movie task. Any entry field created from the IRC announcement can be used for filtering. Most commonly used is `irc_category`, but you are free to filter on uploader, size or whatever else information is available.

`task` is simpler and will send all entries to the task(s). The filtering will have to be done in the tasks. If your tracker is specialized (eg. exclusively TV), then `task_re` might be overkill.

The categories are different for each tracker (maybe not even called `irc_category`, check the tracker file), but usually they match the category names on their website. You could also just monitor the announcements made in their IRC to understand the pattern.

### Example config
```
irc:
  irc_cool_tracker:
    tracker_file: 'MyFunTracker.tracker'
    nickname: 'flexget_bot' #make sure to check naming conventions before joining
    nickserv_password: '{{ secrets.irc.nickserv_password }}'
    port: 7011
    rsskey: '{{ secrets.irc.rsskey }}'
    task: get_entry
    channels: ["#myannounces"]
  irc_some_other_tracker:
    tracker_file: 'MyOtherFunTracker.tracker'
    nickname: 'flexget-bot'
    nickserv_password: '{{ secrets.other_irc.nickserv_password }}'
    passkey: '{{ secrets.other_irc.passkey }}'
    task_re:
      get_tv_entry_with_tracking:
        - regexp: (TV\/x265)|(TV\/x264)|(TV\/Web-DL)
          field: irc_category
      get_movie_entry:
        - regexp: Movie
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
      account: '{{ secrets.trakt.usr }}'
    if:
      - trakt_watched: reject
    manual: yes
    metainfo_series: yes
    thetvdb_lookup: yes
    configure_series:
      from:
        trakt_list:
          account: '{{ secrets.trakt.usr }}'
          list: '{{ secrets.trakt.tv }}'
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
          account: '{{ secrets.trakt.usr }}'
          list: watchlist
    imdb_lookup: yes
    imdb_required: yes
    seen_movies: strict
    proper_movies: yes
    if:
      - trakt_collected: reject
```