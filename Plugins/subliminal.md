= Subliminal =

Download subtitles for entries referred to existing video files.

This plugin requires the subliminal library. To install it, run:

{{{
easy_install subliminal
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
    subliminal:
      languages:
        - it
      alternatives:
        - en
        - fr
      exact_match: yes
}}}

== Options ==

||'''Name'''||'''Info'''||'''Description'''||
||languages||Array||List of preferred languages (3-letter ISO-639-3 code)||
||alternatives||Array||List of secondary languages: subtitles in this list are downloaded, but the entry will be processed again until one for the `languages` list is found||
||exact_match||[yes|no]||Yes: precision search, will get only subs matching the video; No: download anything available for the corresponding movie/episode (default: yes)||
