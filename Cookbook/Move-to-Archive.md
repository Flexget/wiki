# Move to Archive - TV shows and Movies 

This will find all your tv shows and movies that are no longer listed in the Deluge torrent client and that were downloaded over a certain amount of days ago and will move the files and their subtitle files to a different folder (Any mounted drive or local cloud folder). 

  * This setup uses **Deluge torrent downloader**, you can change the collecting task `old-deluge` according to your [input plugins](/Plugins#input) requirements. 

  * Each type (Movies or TV shows) need 2 tasks in order to work: 

    1. `old-deluge` gets the list from the deluge client's label and creates a list: `gotdeluge` 

    2. `old-files` gets the files from the filesystem, removes files listed in the `gotdeluge` list and any that are younger then the 15 days. Remaining media files are moves to the new destination along with subtitle files. 

##  old-deluge Tasks 

  * Replace `<deluge config path>` with the path to your deluge config folder as explained in the plugin [from_deluge](/Plugins/from_deluge). 

  * Change the Deluge label accordingly. 

## old-files Tasks 

  * Replace `<download path>` with the path to the location where your files are. 

  * Change `age: 15 days` to your decided time limit. 

  * Replace `<archive path>` with the path to the location where your archive is. 

  * Under `extensions:` you can add other file extension types that if they have the same name will be copied along with the media file. 

  * This setup will move the file types `avi|mkv|mp4|m4v` change according to your needs.
  * If the source folder size is under 10mb after copying it will be deleted - change `clean_source:` from [move](/Plugins/move) as wanted. - **Be careful**
  

### Copying takes time
  * Do not run these tasks to often - I run once every 24h
### May cause a loss of files - Be carful!
  * I take no responsibility of any damage or anything else anything here may cause - this works on my setup it may not work on yours.
  * Large number of files may be copied
  * Large amount of disk size may be moved - Do you have the space?
  * Large files may be copied
  * If the file is synced/cloud/... Will your network manage?
  * The script uses the OS Move - it may fail and cause a loss of data
  * If you copy to a Null location you may lose your data
  * Moving files is the same as if you moved them manually - consider how and when to run!
  

```
tasks:
  old-deluge-tv:
    priority: 1
    disable:
      - seen
      - seen_info_hash
      - retry_failed
      - builtins
    list_clear:
      what:
        - regexp_list: gotdelugetv
    from_deluge:
      config_path: '<deluge config path>'
      filter:
        label: 'TV'
    accept_all: yes
    list_add:
      - regexp_list: gotdelugetv
    manipulate:
      - title:
          replace:
            regexp: ' '
            format: '.*'

  old-deluge-movies:
    priority: 2
    disable:
      - seen
      - seen_info_hash
      - retry_failed
      - builtins
    list_clear:
      what:
        - regexp_list: gotdelugemovies
    from_deluge:
      config_path: '<deluge config path>'
      filter:
        label: 'Movies'
    accept_all: yes
    list_add:
      - regexp_list: gotdelugemovies

       
  old-files-tv:
    priority: 3
    seen: no
    filesystem:
      path: '<tv download path>'
      recursive: yes
      regexp: '.*.(avi|mkv|mp4|m4v)$'
    metainfo_series: yes
    list_match:
      from:
        - regexp_list: gotdelugetv
      remove_on_match: no
      single_match: no
      action: reject
    accept_all: yes
    require_field: series_name
    age:
      field: created
      action: accept
      age: 15 days
    if:
      - "'Sample' in title": reject
    move:
      to: '<tv archive path>\{{ series_name }}\''
      allow_dir: yes
      clean_source: 10
      along:
        extensions:
          - srt
                
  old-files-movies:
    priority: 4
    seen: no
    filesystem:
      path: '<movie download path>'
      recursive: yes
      regexp: '.*.(avi|mkv|mp4|m4v)$'
    metainfo_movie: yes
    list_match:
      from:
        - regexp_list: gotdelugemovies
      remove_on_match: no
      single_match: no
      action: reject
    age:
      field: created
      action: accept
      age: 15 days
    if:
      - "'Sample' in title": reject
    require_field: movie_name
    move:
      to: '<movie archive path>\{{ movie_name }}\''
      allow_dir: yes
      clean_source: 10
      along:
        extensions:
          - srt
```
Uses plugins:
  * [template](/Plugins/template) - was **not** used in order for easier understanding. Can be used to cut down on the amount of repeating lines.
  * [priority](/Plugins/priority) - in order for the tasks to run in the  proper order.
  * [disable](/Plugins/disable) - used so that every run will not take into consideration any previous runs of the task. Every Deluge pull will get all files listed.
  * [list_clear](/Plugins/List/list_clear) 
  * [from_deluge](/Plugins/from_deluge)
  * [accept_all](/Plugins/accept_all)
  * [list_add](/Plugins/List/list_add)
  * [manipulate](/Plugins/manipulate)
  * [seen](/Plugins/seen)
  * [filesystem](/Plugins/filesystem)
  * [metainfo_series](/Plugins/metainfo_series)
  * [list_match](/Plugins/List/list_match)
  * [require_field](/Plugins/require_field)
  * [if](/Plugins/if)
  * [move](/Plugins/move)
  * [metainfo_movie](/Plugins/metainfo_movie)
  * [age](/Plugins/age)

[Back to The Cookbook](/Cookbook)