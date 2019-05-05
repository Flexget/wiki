tasks:
  task-a:
    rss: http://showrss.info/user/211686.rss?magnets=true&namespaces=true&name=null&quality=null&re=null
    all_series: yes
    transmission:
      host: localhost
      port: 9091
      username: transmission
      password: transmision
      path: :/mnt/dietpi_userdata/downloads/TV/{{series_name}}/Season {{series_season}}
      addpaused: no