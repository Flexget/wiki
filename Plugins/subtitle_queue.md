= Subtitle Queue =

Queue files and download subtitles. Available since v1.2.256. No command line features as of yet (may come later).

== Features ==

 * Download multiple subtitles in different languages
 * Supports Jinja2 templating.
 * Queue the contents of torrents.
 * Use multiple queue tasks to queue files with different languages eg. one queue task to get only english subtitles for some files and another to get strictly swedish for other files.

== Plugin Settings ==

Currently the following settings are supported:
||'''Name'''||'''Info'''||'''Description'''||
||'''action'''||[add|remove]|| Add or remove items to/from the queue. ||
||'''stop_after'''|| interval || Stop retrying after x days/hours/minutes/etc. ||
||'''path'''||string||The path for the file. Supports Jinja2. ||
||'''alternate_path'''||string||An alternative path for the file. Supports Jinja2. ||
||'''languages'''||string or array||Either a single language or a list of languages (as IETF codes).

'''Examples:'''

{{{
subtitle_queue:
  action: add
  languages: en
  path: {{ path }}
  stop_after: 10 days
}}}

{{{
subtitle_queue: emit
subliminal:
  languages:
    - eng
}}}

You can use the {{{add}}} action in a task that downloads files or moves files. Here is an example of two complete tasks:

{{{
Fetch subs:
  template: no_global
  disable_builtins: [retry_failed]
  seen: local
  subtitle_queue: emit
  subliminal:
    exact_match: yes
    languages:
      - eng

Get tvshows:
  set:
    path: /media/downloads
    movedone: /media/tv
  configure_series:
    from:
      trakt_list:
        username: <username>
        password: <password>
        list: custom-tv-list
        type: shows
    settings:
      quality: 720p
  subtitle_queue:
    action: add
    path: "{{path}}"
    alternate_path: "{{movedone}}"
}}}

== Related plugins ==

These plugins work nicely with the {{{emit}}}

 * [wiki:Plugins/subliminal subtitles_subliminal] - Download subtitles with Subliminal.

== Notes ==

 * This plugin has not been tested very thoroughly. Please submit a ticket if something goes wrong.
 * It can take a while before someone creates a subtitle for some videos. It is adviceable to disable [wiki:Plugins/retry_failed retry_failed] in the emit task.
 * There are {{{seen}}} clashes in queue and emit. It may be necessary to disable {{{seen}}} or at least use {{{seen: local}}} in the task.
 * Plugin supports {{{content_filename}}} but it is restricted. If no {{{alternate_path}}} is specified, then it will set the alternate path to {{{path}}} and use {{{content_filename}}} as the filename. If both paths are specified, then it will only apply {{{content_filename}}} to the {{{alternate_path}}}. Has not been tested though.