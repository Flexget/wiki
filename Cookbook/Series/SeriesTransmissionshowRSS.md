tasks:
  # downloading task
  download-rss:
    rss: http://showrss.info/user/100395.rss?magnets=true&namespaces=true&name=null&quality=null&re=null
    # fetch all the feed series
    all_series: yes
    # use transmission to download the torrents
    transmission:
      host: localhost
      port: 9091
      username: matthew
      password: Jonathan1
      addpaused: no