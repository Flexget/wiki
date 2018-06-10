# Move to Archive - TV shows and Movies
This will find all your tv shows and movies that are no longer listed in the Deluge torrent client and that were downloaded over 15 days ago (in this example) and will move the files and there subtitle files (srt only in this example) to a different folder (this can be to any mounted drive or local cloud folder).

  * Each type (Movies or TV shows) include two tasks in order to work:
  1. old-deluge gets the list from the deluge client's label and creates a list: gotdeluge
  2. old-files gets the files from the filesystem, removes files listed in the gotdeluge list and any that are younger then the 15 days. Remaining madia files are moves to the new destionation along with subtitle files.
##  old-deluge Tasks
  * Replace `<deluge config path>` with the path to your deluge config folder as explained in the pligin [from_deluge](/Plugins/from_deluge).
  * Change the Deluge label accordingly.
## old-files Tasks
  * Replace `<download path>` with the path to the location where your files are.
  * Change `days=15` to your decided time limit.
  * Replace `<archive path>` with the path to the location where your archive is.
  * Under `extensions:` you can add other file extension types that if they have the same name will be copied along with the media file.
  * This setup will move the file types `avi|mkv|mp4|m4v` change according to your needs.
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
    if:
      - 'created > now - timedelta(days=15)': reject
      - "'Sample' in title": reject
    move:
      to: '<tv archive path>\{{ series_name }}\'
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
    if:
      - 'created < now - timedelta(days=15)': accept
      - "'Sample' in title": reject
    require_field: movie_name
    move:
      to: '<movie archive path>{{ movie_name }}\'
      allow_dir: yes
      clean_source: 10
      along:
        extensions:
          - srt
```
Uses plugins:
  
  * [priority](/Plugins/priority)
  * [disable]()
  * [list_clear]()
  * [from_deluge]()
  * [accept_all]()
  * [list_add]()
  * [manipulate]()
  * [seen]()
  * [filesystem]()
  * [metainfo_series]()
  * [list_match]()
  * [require_field]()
  * [if]()
  * [move]()
  * [metainfo_movie]()

[Back to The Cookbook](/Cookbook)