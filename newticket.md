tasks:
 kf:
    rss: http://pt.keepfrds.com/torrentrss.php?rows=5
    accept_all: yes
    content_size:
      min: 256
      max: 5200
    download: /home/transmission/torrents
    transmission:
      host: localhost
      port: 9091
      username: cokan
      password: "447964"
    clean_transmission:
      host: localhost
      port: 9091
      username: cokan
      password: "447964"
      finished_for: 12 hours
      tracker: pt.keepfrds.com/
      delete_files: Yes      
    free_space:
      path: /home/transmission/Downloads
      space: 3072