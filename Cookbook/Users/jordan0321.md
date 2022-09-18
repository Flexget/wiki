---
title: jordan0321
description: 
published: true
date: 2022-09-18T05:23:10.820Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:23:08.170Z
---

This is my current flexget configuration. I'll update this to add comments and explanations soon.

Here are some things to know about my motivation for this configuration:
* My wife and I have about 60+ shows between the two of us that we download
* My son is a fan of
  * CFL - Saskatchewan Roughriders
  * NFL - Seattle Seahawks and New York Jets
  * NHL - Pittsburgh Penguins and Winnipeg Jets

```
jordan@claire:~/.flexget$ cat config.yml
templates:
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
    template:
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
    template:
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
    template:
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
    template:
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
    template:
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
    template:
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
    template:
      - emailinfo

```

My email template:
```
jordan@claire:~/.flexget$ cat templates/showrss.template:
{% if task.accepted -%}
{{task.accepted|length}} new torrent(s) has/have just been added:
{%- for entry in task.accepted %}
- {{entry.title}} {% if entry.output|d(false) %} => {{entry.output}}{% endif %}
{% endfor %}
{% endif -%}
```

The contents of the ~Series_To_RSS folder:
```
jordan@claire: ls -l /mnt/big1/tvshows/~Series_To_RSS
total 0
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 America's Next Top Model*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Arrow*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Being Human US*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Blue Bloods*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Burn Notice*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Canada's Next Top Model*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Castle*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Chicago Fire*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Comic Book Men*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Community*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Cougar Town*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Covert Affairs*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 CSI*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Dexter*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Downton Abbey*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Elementary*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Face Off*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Family Guy*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Futurama*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Game of Thrones*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Girls*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Grey's Anatomy*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Hawaii Five-O*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Hot in Cleveland*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 How I Met Your Mother*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Justified*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Longmire*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Louie*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Mike and Molly*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Modern Family*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Mythbusters*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 New Girl*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Nikita*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Once Upon a Time*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Orphan Black*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Penn and Teller Fool Us*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Perception*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 QI*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Raising Hope*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Rizzoli and Isles*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Rookie Blue*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Royal Pains*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Saturday Night Live*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Scandal*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Sherlock*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Sons of Anarchy*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Star Trek Renegade*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Suits*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Supernatural*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Take Me Out*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 The Big Bang Theory*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 The Colbert Report*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 The Daily Show*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 The Glades*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 The Good Wife*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 The IT Crowd*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 The Mentalist*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 The Mindy Project*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 The Simpsons*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 The Walking Dead*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Through The Wormhole*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 True Blood*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Warehouse 13*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 Wedding Band*
-rwxrwxr-x   1 jordan users     0 Aug 31 20:50 White Collar*

```