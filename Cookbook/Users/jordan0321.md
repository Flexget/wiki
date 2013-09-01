{{{
presets:
  clairetransmission:
    transmission:
      host: localhost
      port: 9091
      username: xxxxxxxxx
      password: xxxxxxxxxx

  emailinfo:
    email:
      from: show-notifier@home.xxxxxxxx.ca
      smtp_host: smtp.xxxxxxx.net
      smtp_port: 587
      smtp_username: xxxxxxx
      smtp_password: xxxxxxx
      smtp_tls: no
      template: showrss.template

  privatetracker:
    transmission:
      bandwidthpriority: 1
      ratio: -1

tasks:
  showrss_jordan:
    rss: http://showrss.karmorra.info/rss.php?user_id=xxxxx&hd=null&proper=1&magnets=true
    accept_all: yes
    all_series:
      upgrade: yes
    preset:
      - clairetransmission
      - emailinfo
    email:
      to:
        - jordan@xxxxxxxx.ca

  showrss_christy:
    rss: http://showrss.karmorra.info/rss.php?user_id=xxxxx&hd=null&proper=1&magnets=true
    accept_all: yes
    all_series:
      upgrade: yes
    preset:
      - clairetransmission
      - emailinfo
    email:
      to:
        - christy@xxxxxxxx.ca

  tstn_nfl:
    rss: http://www.thesportstorrentnetwork.co.uk/rss.php?cat=27
    headers:
      Cookie: "uid=xxxxx; pass=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    regexp:
      accept:
        - seahawks
        - jets
      reject:
        - french
    preset:
      - clairetransmission
      - emailinfo
      - privatetracker
    transmission:
      path: /mnt/big1/sports/NFL
    email:
      to:
        - jordan@xxxxxxxx.ca

  tstn_nhl:
    rss: http://www.thesportstorrentnetwork.co.uk/rss.php?cat=1
    headers:
      Cookie: "uid=xxxxx; pass=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    regexp:
      accept:
        - penguins
        - jets
      reject:
        - french
    preset:
      - clairetransmission
      - emailinfo      
      - privatetracker
    transmission:
      path: /mnt/big1/sports/NHL
    email:
      to:
        - jordan@xxxxxxxx.ca

  privatetrackers:
    inputs:
      - rss: https://revolutiontt.me/rss.php?feed=dl&cat=7,41,42&passkey=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
      - rss: http://speed.cd/get_rss.php?feed=dl&user=xxxxxxxxxxxx&cat=2,49&passkey=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
      - rss: http://www.torrentday.com/torrents/rss?download;l24;l26;l7;l2;u=xxxxxxx;tp=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    import_series:
      settings:
        upgrade: yes
      from:
        listdir: /mnt/big1/tvshows/~Series_To_RSS
    preset:
      - clairetransmission
      - emailinfo
      - privatetracker
    email:
      to:
        - christy@xxxxxxxx.ca
        - jordan@xxxxxxxx.ca

  tyt_cfl:
    form:
      url: http://tenyardtracker.com/members.php?action=login
      username: xxxxxxxx
      password: xxxxxxxxxx
    html:
      url: http://tenyardtracker.com/browse.php?c3=1&incldead=1
      title_from: link
    regexp:
      accept:
        - roughriders
      reject:
        - french
    urlrewrite:
      sitename:
        regexp: details.php\?id=(?P<id>\d+).*
        format: download.php?torrent=\g<id>
    preset:
#      - clairetransmission
      - emailinfo
#    transmission:
#      bandwidthpriority: 1
#      ratio: -1
#      path: /mnt/big1/sports/CFL
    download: /mnt/big1/torrents/
    email:
      to:
        - jordan@xxxxxxxx.ca

  appletrailers:
    apple_trailers: 720p
    accept_all: yes
    set:
      filename: "{{ now|formatdate('%Y%m%d') }} - {{ movie_name }} - {{ apple_trailers_name }}.mov"
    download: /mnt/big1/movies/~Trailers
    email:
      to:
        - jordan@xxxxxxxx.ca
        - christy@xxxxxxxx.ca 
    preset:
      - emailinfo

}}}