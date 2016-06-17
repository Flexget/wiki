= Subtitle list =

This plugin is a [wiki:Plugins/List list] plugin.

The main purpose of this plugin is to keep track of local video files that are in need of subtitles. While it allows directories (if specified in config), it's a bit finicky. If you experience any issues, be it unexpected behaviour or bugs, report it on our Github page (http://github.com/Flexget/Flexget).
[[BR]]

'''Notes:''' 

 * subliminal >=2.0rc1 is required for this plugin to work properly.
 * This plugin should be used together with [wiki:Plugins/subliminal subliminal] plugin.
 * If you wish to allow directories, it's important to remember to specify `allow_dir: yes` in all occurrences of `subtitle_list` eg.:
{{{
subtitle_list:  # as input
  list: subtitles
  allow_dir: yes
list_queue:  # accept and remove files from the list if subtitle(s) was found
  subtitle_list:
    list: subtitles
    allow_dir: yes
}}}

== Plugin Settings ==

Currently the following settings are supported:

{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''list'''||User specified name of the list eg. "ru subtitles"||
||'''languages'''||A list of IETF language codes eg. 'en', 'ru' (a complete list: http://data.okfn.org/data/core/language-codes#resource-language-codes)||
||'''check_subtitles'''||Check for existing subtitles be it internal or external (requires subliminal >=2.0rc1).||
||'''remove_after'''||The interval after which the file should be removed from the list -- format: [n] [minutes|hours|days|months] eg. "7 days".||
||'''path'''||The path to save in the list. Can either be a relative or full path. Supports jinja replacement. If it's not set, it will attempt to use the entry's location field. See below for example usage.||
||'''allow_dir'''||Whether to allow the path to be a directory.||
||'''force_file_existence'''||Check for file existence when adding to list and using the list as input. Removes non-existent files/dirs from the list if "yes".||


=== Example: Add video files while moving ===

This example shows how you would use subtitle_list in a task that sorts episodes based on their series_name.

{{{
  move_shows:
    metainfo_series: yes 
    filesystem:
      path:
        - ~/Downloads
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
      retrieve: files
    thetvdb_lookup: yes
    accept_all: yes
    move:
      to: /some/path/{{ series_name }}
    list_add:
      subtitle_list:
        list: subtitles
        languages:
          - en
        path: '{{ output }}'
}}}

=== Example: Download subtitles ===

This example shows how to use the files in a subtitle list along with [wiki:Plugins/subliminal subliminal] to download subtitles.

{{{
  get_subs:
    no_entries_ok: yes
    subtitle_list:
      list: subtitles
    list_queue:
      subtitle_list:
        list: test
    subliminal:
      languages:  # languages is required, but if a language is specified in subtitle_list, it takes priority
        - en
      providers: 
        - addic7ed
        - opensubtitles
        - podnapisi
        - tvsubtitles
      single: no  # will append the language code to the subtitle file
      exact_match: no
}}}