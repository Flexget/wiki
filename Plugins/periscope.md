= Periscope =

Download subtitles for entries referred to existing video files.

This plugin requires the periscope library. To install it, run:

{{{
easy_install periscope
}}}

'''Example (complete task):'''

{{{
  subtitles:
    find:
      path: 
        - d:\media\incoming
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
    accept_all: yes
    periscope:
      languages:
        - it
      alternatives:
        - en
        - fr
      overwrite: yes
}}}

== Options ==

||'''Name'''||'''Info'''||'''Description'''||
||languages||Array||List of preferred languages: must be a ISO 639-1 code (2 digits)||
||alternatives||Array||List of secondary languages: subtitles in this list are downloaded, but the entry will be processed again until one for the `languages` list is found||
||subexts||Array||List of subtitles file extensions to check (for `overwrite` exclusive use)||
||overwrite||[yes|no]||Ignore videos already subbed (check for file with the extensions defined in the `subexts` list)||
