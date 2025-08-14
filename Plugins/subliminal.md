---
title: subliminal
description: 
published: true
date: 2025-08-14T03:54:59.887Z
tags: dependencies
editor: markdown
dateCreated: 2022-09-18T05:13:36.421Z
---

# Subliminal

## Prerequisites
- The `subliminal` extra provided by FlexGet is installed.
  ```
  pip install flexget[subliminal]
  ```

Download subtitles for entries referring to existing video files. 

### Options

| **Name** | **Info** | **Description** |
| --- | --- | --- |
| languages | list | List of preferred languages (as IETF codes) |
| alternatives | list | List of secondary languages: subtitles in this list are downloaded, but the entry will be processed again until one for the `languages` list is found |
| exact_match | [yes\|no] | Yes: precision search, will get only subs matching the video; No: download anything available for the corresponding movie/episode (default: yes) |
| providers | list | List of providers from where to download subtitles.<br>Currently supported: legendastv, shooter, podnapisi, tvsubtitles, opensubtitles, addic7ed, subscenter, thesubdb|
| single | [yes\|no] | Download subtitles in single mode (no language code added to subtitle filename) (default: yes) |
| hearing_impaired | [yes\|no] | Download subtitles for the hearing impaired when available (default: no) (Flexget 2.20 or newer) |
| authentication | dict | Set authentication options for providers that require it (currently `addic7ed`, `legendastv` and `opensubtitles`). Each key should be the provider name, associated with `username` and `password` keys, as in the complete example above (Flexget 2.20 or newer) |


### Example (complete task)

```
tasks:
  get-subtitles:
    filesystem:
      path: 
        - d:\media\incoming         # on Windows
        - /volume/incoming          # unix
      regexp: '.*\.(avi|mkv|mp4)$'  # only include filenames with these extensions
      recursive: yes
    accept_all: yes
    seen: local                     # seen shouldn't interfer with anything outside this subtitles task
    subliminal:
      languages:
        - ita
      alternatives:
        - eng
      exact_match: yes
      # only use the following providers
      providers: [addic7ed, opensubtitles, tvsubtitles]
      single: no
      hearing_impaired: yes
      authentication:               # consider using the variables plugin
        addic7ed:
          username: my_user
          password: my_password
        opensubtitles:
          username: other_user
          password: other_passsword
```

### Notes

With respect to single mode, if more than one language is provided in the configuration, then language codes are added to the potentially downloaded subtitles

Options `alternatives`, `exact_match`,  `providers`, `single`, `hearing_impaired` and `authentication` are optional.

Omitting `providers` means all available providers will be used, which includes the ones that that don't need authentication, or that have been properly configured with the `authentication` option.

### Related

- Consider making use of the [`variables` plugin](/Plugins/variables) to store the usernames and passwords outside of the main configuration file.
- [periscope plugin](/Plugins/periscope)
- Works well together with the [`filesystem` plugin](/Plugins/filesystem)