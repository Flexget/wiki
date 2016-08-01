# Subliminal
Download subtitles for entries referred to existing video files.

This plugin requires the subliminal >=2.0rc1 library. To install it run the follwing

```cmd
pip install subliminal==2.0rc1
```

**Example (complete task):**

```
tasks:
  get-subtitles:
    filesystem:
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
```

## Options

| **Name** | **Info** | **Description** |
| --- | --- | --- |
| languages | list | List of preferred languages (as IETF codes) |
| alternatives | list | List of secondary languages: subtitles in this list are downloaded, but the entry will be processed again until one for the `languages` list is found |
| exact_match | [yes\|no] | Yes: precision search, will get only subs matching the video; No: download anything available for the corresponding movie/episode (default: yes) |
| providers | list | List of providers from where to download subtitles |
| single | [yes\|no] | Download subtitles in single mode (no language code added to subtitle filename) (default: yes) |

#### Notes
With respect to single mode, if more than one language is provided in the configuration, then language codes are added to the potentially downloaded subtitles

Options `alternatives`, `exact_match`,  `providers` and `single` are optional in the configuration file