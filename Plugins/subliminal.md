= Subliminal =

Download subtitles for entries referred to existing video files.

This plugin requires the subliminal v1.0.1 library. To install it, download the following zip file:

{{{
https://github.com/Diaoul/subliminal/archive/master.zip
}}}

unzip it and run

{{{
python setup.py install
}}}

Note: In Unix you may need root privileges

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
        - ita
      alternatives:
        - eng
      exact_match: yes
      providers: [addic7ed, opensubtitles]
      single: no
}}}

== Options ==

||'''Name'''||'''Info'''||'''Description'''||
||languages||Array||List of preferred languages (as IETF codes)||
||alternatives||Array||List of secondary languages: subtitles in this list are downloaded, but the entry will be processed again until one for the `languages` list is found||
||exact_match||[yes|no]||Yes: precision search, will get only subs matching the video; No: download anything available for the corresponding movie/episode (default: yes)||
||providers||Array||List of providers from where to download subtitles||
||single||[yes|no]||Download subtitles in single mode (no language code added to subtitle filename) (default: yes)||

== Notes ==

With respect to single mode, if more than one language is provided in the configuration, then language codes are added to the potentially downloaded subtitles

Options 'alternatives', 'exact_match', 'providers' and 'single' are optional in the configuration file
