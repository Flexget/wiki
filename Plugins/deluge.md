# Deluge

Downloads content from entry URL and loads it into the [deluge](http://deluge-torrent.org) bittorrent client.

<div class="alert alert-warning" role="alert">
<ul>
<li>Deluge requires Python 2.7. It does NOT support Python 3.3+ as of 2017.</li>
<li>
If you are installing to a virtualenv, you have to create the virtualenv with the --system-site-packages option so the deluge package can be found. This also applies to a git install.</li>
<ul>
</div>

**Requirements:**
* Supports Deluge 1.2 and 1.3. This will not work if you are running deluge in classic mode. You must switch to running the daemon separately. 
* If you are running `deluged` as a different user, on a different box, or with a non-default config directory (something other than ~/.config/deluge), you will need to specify the username and password options that you have set up in your Deluge [auth](http://dev.deluge-torrent.org/wiki/UserGuide/Authentication) file.


### Configuration
None of the options are required, and they will all default to whatever you have set in Deluge.

If you do not wish to set any of the parameters the format is:

```yaml
deluge: yes
```

### Options

| **Name** | **Description** |
| --- | --- |
| host | Deluge host (default *localhost*) |
| port | Deluge port (default *58846*) |
| username | Deluged username *(defaults to automatic client authentication if not specified)* |
| password | Deluged password *(defaults to automatic client authentication if not specified)* |
| path | The download location |
| movedone | The location files will be moved when torrent finishes (the location will be created if it doesn't exist). |
| label | Label to assign to torrents in Deluge. This field can be a [Jinja expression](/Jinja) and is rendered before being passed to Deluge. |
| queuetotop | If yes will move torrent to top of queue when added, if no will move to bottom. |
| addpaused | If yes, will add the torrents to deluge in the paused state. |
| maxupspeed | Sets the maximum upload speed. Must be specified as a decimal (i.e. 1.0) |
| maxdownspeed | Sets the maximum download speed. |
| maxconnections | Sets the maximum connections. |
| maxupslots | Sets the maximum upload slots. |
| ratio | Sets the ratio to stop seeding at. |
| removeatratio | If yes, torrent will be removed from deluge when ratio is reached. |
| compact | If yes, will allocate torrent in compact mode. |
| automanaged | If set to false torrents will be added to deluge without the automanaged flag. |
| content_filename | This can be used to rename the main file and directory of the torrent. [see here](/Plugins/deluge#ContentRenaming) |
| main_file_only | If yes, all files but the main file inside the torrent (>90% of total by default) will be set to 'do not download' |
||main_file_ratio|| Sets the threshold value for *main_file_only*. Expects a number between 0 and 1 (ie 0.85 to change to 85%). 90% by default.|
| magnetization_timeout | When the timeout is set greater than 0 and a magnet URI is added, the task will wait up to the timeout (seconds) for the torrent to magnetize before continuing (Default: 0) |
| hide_sparse_files | If *main_file_only* is set, all the other (sparse) files will be put inside a hidden subdirectory (called ".sparse_files"). On by default. |
| keep_subs | If *main_file_only* is set, the subtitle file is also downloaded. If *content_filename* is set, the subtitle file will be renamed too. If *hide_sparse_files* is set, the subtitle will not be hidden. On by default. |

### Example

```yaml
deluge:
  path: /media/diska/downloads/
  movedone: /media/diska/tv/
  label: `{{trakt_series_network}}`
  queuetotop: yes
```

### Advanced
Some plugins allow [set](/Plugins/set) to be applied on matched entries.
The deluge plugin will read any of the normal parameters from the entry fields, except for deluge daemon info (host, port, username, password).
Here is an example using the series module:

Example with set:

```yaml
series:
  settings:
    720p:
      quality: 720p hdtv|webdl
      set:
        path: /media/diska/incomplete/
        movedone: "/media/diska/TV/{{series_name}}/"
        label: 720p
    hdtv:
      quality: hdtv <720p
      set:
        path: /media/diskb/incomplete/
        movedone: "/media/diskb/TV/{{series_name}}/Season {{series_season}}/"
        label: tv
  720p:
    - name 1
    - name 2
  hdtv:
    - name 3
    - name 4:
        set:
          movedone: /media/diskb/otherfolder/
          queuetotop: yes
deluge: yes
```

The more specific set commands will override the less specific ones (i.e. the set command from name 4 will override the set values from the hdtv group.)

### Content Renaming
The deluge plugin also supports another advanced feature: content file renaming. This will allow you to change the name of the main file and directory of the torrent in deluge. It will only rename a file/directory if it finds that one file in the torrent is larger than 90% (or specified value) of the total torrent content.

Specifying a directory as part of the content_filename is optional. Not doing so will leave the torrent folder structure alone, just renaming the file.

Here is an example configuration:

```yaml
series:
  settings:
    groupa:
      set:
        content_filename: "{{series_name}} - {{series_id}}/{{series_name}} - {{series_id}} - {{quality}}"
        movedone: /home/user/TV/{{series_name}}/Season {{series_season}}/
  groupa:
    - Show Name
deluge: yes
```

This config uses [Jinja2](/Plugins/set#Jinja2Templating) notation to rename the file using information from the series parser. If there was a file called `Show.Name.9x15.REPACK.720p.HDTV.x264-FOOBAR.mkv` inside the torrent, it would be renamed to `Show Name - S09E15 - 720p.mkv` If there is already a file with the new name present in either the downloading folder, or movedone folder, a trailing number will be added to the filename. i.e. `Show Name - S09E15 - 720p(2).mkv`

Together with the movedone command, this means all TV series will be downloaded to:

```text
/home/user/TV/Show Name/Season #/Show Name - S##E##/Show Name - S##E## - quality.ext
```

Subtitle files will be downloaded to (see the `keep_subs` option):

```text
/home/user/TV/Show Name/Season #/Show Name - S##E##/Show Name - S##E## - quality.srt
```

**NOTE:** In order to perform content renaming on a magnet URI, you must set **magnetization_timeout** to a value greater than 0 so that flexget has a chance to magnetize the torrent and retrieve the file list before performing any file list processing during the content renaming phase. If you use any feeds that supply magnet URIs and you wish to perform content renaming, it is strongly recommended to set **magnetization_timeout** to a reasonable wait period, such as **30** (seconds). Magnetization time varies based on swarm activity and network speed, but is typically completed in under 10 seconds.

## macOS / OSX Users
Should you wish to use the Deluge plugin:
- The default Flexget installation currently requires Deluge to be installed via [macports](http://dev.deluge-torrent.org/wiki/Installing/MacOSX/) (or source).
- Alternatively, if you have Deluge.app:
  - You can use the third-party plugin [`app_deluge_find`](/Plugins/app_deluge_find) by adding `app_deluge_find: yes` to each affected task, which allows FlexGet to recognize /Applications/Deluge.app.
  - You can also edit flexget/plugins/clients/deluge.py to achieve the same effect with the changes noted [here](https://github.com/Flexget/Flexget/issues/1671) made to `flexget/plugins/client/deluge.py`.

## Windows Users
FlexGet should be able to detect Deluge in its install directory if:
- Deluge is installed in the default install directory <program files>\Deluge
- FlexGet and Deluge are installed with 32 bit Python 2.7

You can ignore messages about disconnecting from the daemon in a 'non-clean' fashion. This is normal on Windows.