''Draft. To be approved/corrected by cvium.''

== IRC ==
This plugin will allow you to connect an "autodl" bot to an IRC channel. It listens for release announcements, parses them and sends them to the FlexGet daemon, which executes a task of your choosing with the input from IRC.
It's a somewhat complex plugin and difficult to test without access to the various trackers.

Unlike web crawling like most other search plugins, the bot will instead await torrent announcements in the given IRC channel(s), and will instantly pick any new releases up almost immediately. This benefits both the torrent sites and yourself.

=== Prerequisites ===
* Run Flexget in daemon-mode. (ex: ''flexget daemon start --daemonize''). This means you may want to migrate your cron-jobs to use the scheduler plugin instead.
* irc python package (ex: ''pip install irc'')
* Have a autodl-tracker file relevant to your intended tracker, downloaded from [https://github.com/autodl-community/autodl-trackers here].
* rsskey or other needed credentials located in the tracker file and in the guide sections in your tracker website. (hint: look for autodl guides)

=== Settings ===
||= Option =||= Description =||=Example=||
||'''tracker_file'''|| ''(required, unless server+channels+port are all specified)'' Path to the tracker file you downloaded specifically for your tracker || '/absolute/path/to/trackerfile' ||
||'''task'''|| ''(required)'' Task to execute and send entry to ||get_entry ||
||'''nickname'''|| ''(required)'' Specify your nickname. Careful to follow tracker conventions or get banned. ||myusername-bot ||
||'''server'''|| Explicitly specify server address || irc.someplace.net ||
||'''port'''|| Explicitly specify port number (integer) || 6667 ''(default)'' ||
||'''channels'''|| Explicitly specify announce channel(s). Joining channels that are not announce-channels can get you banned. ||!['#announce_channel'] ||
||'''nickserv_password'''|| Password for authenticating your nickname to nickserv || ||
||'''invite_nickname'''|| Some trackers use this for extra authentication || ||
||'''invite_message'''|| Some trackers use this for extra authentication || ||
||'''queue_size'''|| Throttle IRC torrent announcements in case of spam. || 1 ''(default)'' ||

=== Example config ===
{{{
irc:
  irc_cool_tracker:
    tracker_file: '/absolute/path/to/trackerfile'
    nickname: 'qvazzler_autodl' #make sure to check naming conventions before joining
    nickserv_password: '{{ secrets.irc.nickserv_password }}'
    port: 7011
    rsskey: '{{ secrets.irc.rsskey }}'
    task: cool_tracker_get
    channels: ["#ctannounces"]
  irc_some_other_tracker:
    tracker_file: '/absolute/path/to/a/different/trackerfile'
    nickname: 'qvazzler-bot' #make sure to check naming conventions, this one is different
    nickserv_password: '{{ secrets.other_irc.nickserv_password }}'
    port: 6667
    passkey: '{{ secrets.other_irc.passkey }}'
    task: some_other_tracker_get
    channels: ["#sot.announce"]

tasks:
  #Passed into this task with very few fields available, including title, download url, and the fields from the tracker file..
  cool_tracker_get:
    metainfo_series: yes
    #trakt_lookup: yes # do I need this?
    disable: seen
    if:
      - irc_category in ['Movies', 'TV/HD', 'TV/SD']: accept
    ..
    ..
    .. download ..
}}}


=== Known Issues ===
* May fail to reconnect under certain conditions or crash. Should be worked out now that the irc daemon restarts the connection after a very short period.

=== Tips ===
* Fields in the tracker file for you to use if/regex with in the task are prefixed with {{{ irc_ }}}. Example: {{{ irc_category }}}
* Passkey, rsskey, user, uid, the fields you need to specify all vary depending on the tracker, not do they originate from the irc daemon. Pay extremely close attention to the trackerfile.
* If you are using multiple configs, you'll need to use daemon on all of them, then combine exec, some bash scripting, web ui and web api to distribute the announce event to the different flexget daemons running diff. configs.
* It is _technically_ possible to run this without a tracker file, but then you'd lose the irc_ prefixed fields. If the message is more than an URL, be prepared to use the manipulate plugin.
* cvium is still accepting bug reports. This functionality should still be considered experimental.