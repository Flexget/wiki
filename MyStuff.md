tasks:
  showrss task:
    rss: http://showrss.info/user/77481.rss?magnets=true&namespaces=true&name=null&quality=null&re=null
    all_series: yes
    deluge:
      path: F:/Media/TVShows/Downloading
      movedone: F:/Media/TVShows/{{series_name}}/Season {{series_season}}
      main_file_only: true
      removeatratio: true