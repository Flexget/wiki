task:
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