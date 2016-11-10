# rTorrent

This plugin adds URL's directly into rTorrent or create entries from rTorrent for further automation.

**Supports**

* Protocols XMLRPC, SCGI and Local SCGI
* Dynamically setting the download directory and custom attributes supporting [jinja replacement](/Jinja)
* Magnet urls
* Digest authentication (if 401 error code is returned, it falls back to either Basic or Digest depending on config setting)

## Syntax


```yaml
rtorrent:
  uri: scgi://localhost:5000
  path: /data/torrent/ongoing/
  custom1: TV
```

## Options
**Common Options**


| **Name** | **Info** | **Description** |
| --- | --- | --- |
| uri | Text | rTorrent URI. IE: scgi://localhost:5000, http://localhost:80/RPC2, /home/rtorrent/rtorrent.sock  |
| username | Text | Username when using HTTP for basic auth |
| password | Text | Password when using HTTP for basic auth |
| digest_auth | [yes\|no] | Use Digest authentication |
| timeout | Text | Seconds before timeout when connecting to rtorrent |

**Output specific options**


| **Name** | **Info** | **Description** |
| --- | --- | --- |
| mkdir | [yes\|no] | Create the destination folder on the rTorrent server (default: yes) |
| start | [yes\|no] | Automatically start newly added torrent (default: yes) |
| action | [add\|update\|delete] | Default is add |
| path | Directory | Destination for downloaded file(s). Supports [jinja replacement](/Jinja). <br>**Note:** Will contain incomplete ongoing downloads.|
| priority | [off\|low\|medium\|high] | Set torrent priority (default off) |
| custom1 | Text | Set custom field |
| custom2 | Text | Set custom field |
| custom3 | Text | Set custom field |
| custom4 | Text | Set custom field |
| custom5 | Text | Set custom field |

**Input specific options**


| **Name** | **Info** | **Description** |
| --- | --- | --- |
| view | Text | View to use as input (default main) |
| fields | list | specify which fields to get from rtorrent. See below for default fields |

The following entry fields are set by default on input.

- torrent_info_hash
- title
- up_total
- down_total
- down_rate
- is_open
- is_active
- custom1
- custom2
- custom3
- custom4
- custom5
- state
- complete
- bytes_done
- down_rate
- left_bytes
- ratio
- path


### Example
Use fields to remove after 2.0 ratio and above

```yaml
tasks:
  delete-ratio:
    from_rtorrent:
      uri: scgi://localhost:5000
    if:
      - ratio > 2.0: accept
    rtorrent:
      action: delete
      custom2: complete
      uri: http://192.168.0.20/rtorrent
```


### Example: Move completed  1

Create rTorrent action on complete

File .rtorrent.rc

```
system.method.set_key = event.download.finished,move_complete,"execute=mv,-u,$d.get_base_path=,$d.get_custom1=;d.set_directory=$d.get_custom1="
```

Add TVShows to rTorrent and set the download directory to `/data/downloads/TV/{{ tvdb_series_name }}`

```yaml
tasks:
  tv:
    rss: http://domain/rss.xml
    accept_all: yes
    rtorrent:
      uri: scgi://localhost:5000
      path: /data/downloads/ongoing/
      custom1: /data/downloads/TV/{{ tvdb_series_name }}
```

### Example: Move completed  2

**NOTE:** Unsure how/if this works, original rTorrent plugin author wrote this so it probably does ...

Add TVShows to rTorrent and set the download directory to `/data/downloads/TV/{{ tvdb_series_name }}`

```yaml
tasks:
  tv:
    rss: http://domain/rss.xml
    accept_all: yes
    rtorrent:
      uri: scgi://localhost:5000
      path: /data/downloads/TV/{{ tvdb_series_name }}
      custom1: TV
```

Once downloaded move to another folder. You can obviously expand on this config to auto extract (using the decompress plugin) and rename the files then keep seeding.

```yaml
tasks:
  move-complete:
    from_rtorrent:
      uri: scgi://localhost:5000
    regexp:
      accept_excluding:
        - complete
      from: custom2
    rtorrent:
      action: update
      custom2: complete
      uri: http://192.168.0.20/rtorrent
      path: /data/seeding/{{ custom1 }}/{{ tvdb_series_name }}
```