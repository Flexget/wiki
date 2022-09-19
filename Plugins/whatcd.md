---
title: whatcd
description: 
published: true
date: 2022-09-18T05:16:49.394Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:16:46.771Z
---

# what.cd
[Includes/PluginRemovedArchived](/Includes/PluginRemovedArchived){.include}

A plugin that performs searches on [https://what.cd](/https://what.cd) and returns entries for each result.

## Usage
All parameters except `username` and `password` are optional.

```
whatcd:
    username:     # What.cd username
    password:     # What.cd password

    user_agent:   # A custom user-agent for the client to report.
                  # It is NOT A GOOD IDEA to spoof a browser with
                  # this. You are responsible for your account.
                  # By default it's "Flexget (What.cd plugin)"

    search:       # General search filter

    artist:       # Artist name
    album:        # Album name
    year:         # Album year

    encoding:     # Encoding specifics. One of:
                  # '192', 'APS (VBR)', 'V2 (VBR)', 'V1 (VBR)', '256', 'APX (VBR)',
                  # 'V0 (VBR)', '320', 'lossless', '24bit lossless', 'V8 (VBR)'

    format:       # File format. One of:
                  # 'MP3', 'FLAC', 'AAC', 'AC3', 'DTS'

    media:        # Media type. One of
                  # 'CD', 'DVD', 'vinyl', 'soundboard', 'SACD', 'DAT', 'cassette',
                  # 'WEB', 'Blu-ray'

    release_type: # The release type. One of:
                  # 'album', 'soundtrack', 'EP', 'anthology', 'compilation',
                  # 'DJ mix', 'single', 'live album', 'remix', 'bootleg',
                  # 'interview', 'mixtape', 'unknown', 'concert recording', 'demo'

    log:          # Log specification. One of:
                  # true, false, '100%', or '<100%'

    hascue:       # Has a cue file - true or false
    scene:        # Is a scene release - true or false
    vanityhouse:  # Is a vanity house release - true or false
    leech_type:   # The leech type. One of
                  # 'freeleech', 'neutral', 'either', or 'normal'

    tags:         # A list of tags to match. These are the tags on What.cd
                  # Example: ['drum.and.bass', 'new.age', 'blues']

    tag_type:     # The type of matching to use on the tags.
                  # Can be 'any' or 'all'
```

## Example
Find all non-scene lossless FLAC CD rips from 2000 with a perfect log file

```
whatcd:
    username: myusername
    password: mypass

    year: 2000
    encoding: lossless
    format: FLAC
    media: CD
    log: 100%
    scene: false
```