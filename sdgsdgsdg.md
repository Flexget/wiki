tasks:
  download_kent_rss:
    priority: 10
    template:
      - disable-seen-retry
      - kent_template
      - transmission-kent
      - pushbullet

  download_kdrama_rss:
    priority: 10
    template:
      - disable-seen-retry
      - kdrama_template
      - transmission-kdrama


############ 이동 ############
  move_kent:
    priority: 50
    filesystem:
      path: "/{? folder.down_path ?}{? folder.downkent ?}"
      recursive: yes
      retrieve: files
      regexp: '.*\.(avi|mkv|mp4)$'
    accept_all: yes
    move:
      to: "/{? folder.save_path ?}{? folder.kent ?}"
    exec:
      on_exit:
        phase: find "/{? folder.down_path ?}{? folder.downkent ?}"* -type d -empty -delete

  move_kdrama:
    priority: 51
    filesystem:
      path: "/{? folder.down_path ?}{? folder.downkdrama ?}"
      recursive: yes
      retrieve: files
      regexp: '.*\.(avi|mkv|mp4)$'
    accept_all: yes
    move:
      to: "/{? folder.save_path ?}{? folder.kdrama ?}{{tmdb_name|default(series_name)|pathscrub}}/"
    exec:
      on_exit:
        phase: find "/{? folder.down_path ?}{? folder.downkdrama ?}"* -type d -empty -delete
