tasks:
  task-a:
    rss: http://showrss.info/user/211686.rss?magnets=true&namespaces=true&name=null&quality=null&re=null
    all_series: yes
    transmission:
      host: 192.168.0.23
      port: 9091
      username: transmission
      password: transmission
      path: /mnt/dietpi_userdata/downloads/TV/{{series_name}}/Season {{series_season}}
      addpaused: no