---
title: gazelle
description: 
published: true
date: 2022-09-18T05:17:56.120Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:17:53.398Z
---

# Gazelle-based sites
This family of search plugins will search for torrents on most Gazelle-based websites.

## Plugins
| **name** | **description** |
|---|---|
| `gazelle` | A generic plugin that searches a Gazelle-based website. Limited functionality (just basic search) but should work for almost all of them.|
| `gazellemusic` | A plugin that searches a Gazelle-based music website. Based on the source code for what.cd since it's the starting point of all Gazelle-based music sites.|
| `redacted` | A specialized version of the `gazellemusic` plugin that searches [RED](https://redacted.ch)|
| `notwhatcd` | A specialized version of the `gazellemusic` plugin that searches [NWCD](https://notwhat.cd)|


### Hierarchy
The plugins in the Gazelle family form a hierarchy. The `redacted` and `notwhatcd` plugins are specialized versions of the `gazellemusic` plugin, which, in turn, is a specialized version of the `gazelle` plugin

This can be visualized like so:
```
      gazelle
         |
    gazellemusic
         |
   +-----+-----+
   |           |
redacted   notwhatcd
```

Because of this setup, all functionality and configuration options (except where otherwise noted) from parent plugins also apply to the child plugins.

## Configuration
The only options that are required are `username`, `password`, and `base_url`. Note that plugins that are specialized for a certain domain like `redacted` and `notwhatcd` do not require `base_url` as they will assume it.


### `gazelle`
|**key** | **decription** |
|---|---|
|`username`| The username to log into the site as|
|`password`| The password for the username|
|`base_url`| The site to access (ex: `https://example.org`)|
|`max_pages`| The maximum number of search result pages to return before stopping (defaults to 5)|
|`search`| The search query to run on the site|


### `gazellemusic`
Inherits all options from `gazelle`
|**key** | **decription** |
|---|---|
|`artist`|Artist name|
|`album`|Album name|
|`year`|Year the music was released|
|`encoding`|Music encoding. Options: `192`, `APS (VBR)`, `V2 (VBR)`, `V1 (VBR)`, `256`, `APX (VBR)`, `V0 (VBR)`, `q8.x (VBR)`, `320`, `Lossless`, `24bit Lossless`, `Other`|
|`format`|File format. Options: `MP3`, `FLAC`, `Ogg Vorbis`, `AAC`, `AC3`, `DTS`|
|`media`|The physical media of the release. Options: `CD`, `DVD`, `Vinyl`, `Soundboard`, `SACD`, `DAT`, `Cassette`, `WEB`|
|`release_type`|The release type. Options: `album`, `soundtrack`, `EP`, `anthology`, `compilation`, `single`, `live album`, `remix`, `bootleg`, `interview`, `mixtape`, `unknown`
|
|`leech_type`|Torrent leech type. Options: `freeleech`, `neutral`, `either`, `normal`|
|`tags`|comma-separated music tags|
|`tag_type`|`any` or `all`|
|`hascue`|`True`, `False`|
|`scene`|`True`, `False`|
|`vanityhouse`|`True`, `False`|
|`log`|`True`, `False`, `100%`, `<100%`|

### `redacted`
Inherits all options from `gazellemusic`
|**key** | **decription** |
|---|---|
|`encoding`|Same as `gazellemusic` without `q8.x (VBR)`|
|`format`|Same as `gazellemusic` without `Ogg Vorbis`|
|`media`|Same as `gazellemusic` plus `Blu-ray`|
|`release_type`|Same as `gazellemusic` plus `demo`, `concert recording`, `dj mix`|

### `notwhatcd`
Inherits all options from `gazellemusic`
|**key** | **decription** |
|---|---|
|`media`|Same as `gazellemusic` plus `Blu-ray`, `Unknown`|
|`release_type`|Same as `gazellemusic` plus `demo`, `concert recording`, `dj mix`|
|`log`|Same as `gazellemusic` plus `gold`, `silver`, `gold/silver`, `lineage`, `unscored`, `missing lineage`, `missing dr score`, `missing sample rate`, `missing description`|


## Example tasks
```
tasks:
    nwcd:
        notwhatcd:
            username: myuser
            password: mypass

            artist: SomeArtist
            format: FLAC
            media: CD
            release_type: album
            log: gold/silver
        accept_all: True

    red-flac:
        redacted:
            username: myuser
            password: mypass

            max_pages: 2
            format: FLAC
        accept_all: True

    red-search:
        discover:
            release_estimations: ignore
            what:
              - mock:
                - title: SomeAlbum
              - mock:
                - title: SomeArtist
            from:
              - redacted:
                    username: myuser
                    password: mypass
        accept_all: True

    gazmusic-apl:
        gazellemusic:
            base_url: https://apollo.rip
            username: myuser
            password: mypass

            album: SomeAlbum
            artist: SomeArtist
        accept_all: True
```