This is the personal configuration of user foulou . I will try to remember to update this page when I make changes.

This config grabs many rss feeds and adds movies and TV shows to deluge. I use trakt.tv to mark my downloaded series a get on the site, and use trakt plugin to input my series into flexget.
For movies, I want only DVDrip that are somewhat new.
The last feed is a feed that check a directory for new torrent, and process them into flexget, I use it when flexget miss some episodes, or when I want a new serie that have already some ep out; this way it update flexget, and order ep inside my completed dir.

Plugins used (a ton): trakt, trakt_acquired,series, import_series, imdb, deluge, regexp, form, headers, urlrewite, inputs, exists_series, thetvdb_lookup, imdb_lookup, content_size, seen_movies, imdb_required, exists_movie, quality, preset, accept_all, torrent_alive, private_torrents, email, set.


{{{
presets:
  global:
    email: # I want an email of everything flexget downloads
      from: FlexGet@xxxxxxx
      to:
        - xxxxxxxxxxxx
        - xxxxxxxxxxxxx
      smtp_host: localhost
      smtp_port: 25
    urlrewrite: # some url rewrite
      www.frenchtorrentdb.com:
        regexp: 'http://www.frenchtorrentdb.com/\?section=DOWNLOAD&id=(?P<id>\d+)'
        format: 'http://www2.frenchtorrentdb.com/?section=DOWNLOAD&id=\g<id>'
      www.play-the.net:
        regexp: 'http://www.play-the.net/\?section=INFOS&id=(?P<id>\d+)'
        format: 'https://www.play-the.net/?section=DOWNLOAD&id=\g<id>'
    deluge:
      queuetotop: yes # new torrent on top
      user: xxx
      pass: xxx
    torrent_alive: yes # is the torrent alive ?
  zik: # preset music
    content_filter:
      require:
        - '*.mp3' # I want only mp3 files, no flac or other
    regexp:
      from: title # search only inside the torrent name
      accept: # groups I listen
        - 36 Crazyfist
        - Accept
        - Adramelch
        - After Forever
        - Alkemyst
        - Almah
        - Altaria
        - Amberian Dawn
        - Amorphis
        - Amoral
        - Andre Matos
        - Angra
        - Ankhara
        - Anubis Gate
        - Arkania
        - At Vance
        - Atreyu
        - Avalanch
        - Avantasia
        - Avian
        - Axenstar
        - Axxis
        - Ayreon
        [and more other...]
    set: # move when done changed into deluge
      path: /home/seb/media/Downloads/Torrent/Downloading/
      movedone: "/home/seb/media/Downloads/Torrent/Downloaded/0o__MUSIQUE__o0/"
      label: Zik
  tv: # tv preset
    regexp:
      from: title
      reject: # i don't want any torrent of these 2 teams
        - MiND
        - SSL
    content_filter:
      require: # also I just want avi or mkv, no mp4 or else
        - '*.avi'
        - '*.mkv'
    import_series: # import series into plugin series
      from:
        inputs: 
# what i want to import come from trakt, and i want the watchlist and the all list from the trakt plugin
# when i like a new serie and i want it to be downloaded, i just add it in whatchlist on trakt.tv
# the all is for the series that are not in whatchlist but i whatch.
          - trakt_list:
              username: foulou
              api_key: xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
              series: watchlist
          - trakt_list:
              username: foulou
              api_key: xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
              series: all
      settings:
        quality: HDTV # and i said that everything imported is HDTV category
    series:
      settings: 
# so in series, I have HDTV category, where i add some parameters, like i want propers
# and i want ep in these following qualities.
        HDTV:
          propers: yes
          qualities:
            - hdtv
            - dvdrip
            - bdrip
    thetvdb_lookup: yes
    set: # I order my completed dir with deluge, by setting the move when done parameter.
      path: /home/seb/media/Downloads/Torrent/Downloading/
      movedone: "/home/seb/media/Series/{{ series_name }}/S0{{ series_season }}"
      label: TV
    trakt_acquired: # i mark downloaded ep as acquired on trakt !
      username: foulou
      password: *********
      api_key: *******************
      type: series
    exists_series: # check for existing series inside my dirs
      - /home/seb/media/Downloads/Torrent/Downloaded/
      - /home/seb/media/Series
      - /home/seb/media/Downloads/Torrent/Downloading
  animes: # anime preset
    series:
      settings:
        480p:
          quality: 480p
        360p:
          quality: 360p
      480p:
        - Naruto Shippuuden
        - Fairy Tail
        - Bleach
      360p:
        - One Piece
    thetvdb_lookup: yes
    set: 

# I order them with deluge also, and moreover, I rename them to be compatible with XBMC so SxxExx is needed
# I know i can use ordered numbering into XBMC but i prefer it to be in season.

# '''I need to use http://flexget.com/ticket/1151 to have this work'''

      path: /home/seb/media/Downloads/Torrent/Downloading/
      movedone: "/home/seb/media/Animes/{{ series_name }}/S{{ series_season }}"
      label: Animes
      main_file_only: yes # i just want the bigger file in the torrent
      content_filename: >
        {{ series_name }} - S{{ series_season }}E{{ series_episode }} - {{ ep_name }}
    trakt_acquired: # also mark my anime ep acquired into trakt
      username: foulou
      password: ************
      api_key: **********************
      type: series
    exists_series: # check what i have
      - /home/seb/media/Animes
      - /home/seb/media/Downloads/Torrent/Downloading
  movies: # movie preset
    imdb:
      min_year: 2010 # i want movie not to be older than 2010
      reject_genres: # don't wnat these type of films
        - News
        - Documentary
        - Horror
    quality: #these quality, dvdrip to 720p
      max: 720p
      min: dvdrip
    content_size: # but between 650 and 1000 Mb, so in fact it's only DVDRIP and in 1 file, I hate films splitted into 2 files
      max: 1000
      min: 650
    seen_movies: loose # sometime imdb don't match and i don't want him to reject the movie because of that.
    imdb_lookup: yes
    set:
      label: Movies
      path: /home/seb/media/Downloads/Torrent/Downloading
      movedone: "/home/seb/media/Downloads/Torrent/Downloaded/0o__FILMS__o0/"
    trakt_acquired: #mark movie acquired on trakt
      username: foulou
      password: ************
      api_key: **********************
      type: movies
feeds: # I have a lot of feeds, because of some being private tracker, i cant merge them.
  FTDB_TV:
    headers:
      Cookie: "WebsiteID=***********************" # used to login into the tracker
    form: # used to login into the tracker
      url: http://www2.frenchtorrentdb.com
      username: **************
      password: **************
    rss: http://www2.frenchtorrentdb.com/rss/tv_vostfr.rss
    preset: tv
  FTDB_DVDRIP:
    regexp:
      from: title
      reject: #OK i want only movies in french, so i reject every torrent which have the following in their title
        - VOSTFR
        - V O S T F R
        - V O S T FR
        - Sub FR
    headers:
      Cookie: "WebsiteID=****************" # used to login into the tracker
    form: # used to login into the tracker
      url: http://www2.frenchtorrentdb.com
      username: ********
      password: ************
    rss: http://www2.frenchtorrentdb.com/rss/dvdrip.rss
    preset: movies
  NyaaTorrents:
    rss: http://www.nyaa.eu/?page=rss&cats=1_37&term=horriblesubs&filter=2
    preset: animes
  PTN_TV:
    regexp:
      from: title # i want only VOSTFR Tv shows, and this tracker put a rss with french and VOSTFR show together.
      reject:
        - FRENCH
    headers:
      Cookie: "WebsiteID=************************" # used to login into the tracker
    form: # used to login into the tracker
      url: https://www.play-the.net/
      username: ***************
      password: ****************
      userfield: user
      passfield: pass
    rss: https://www.play-the.net/rss/serie+tv+vostfr.rss
    preset: tv
  PTN_DVDRIP:
    regexp:
      from: title
      reject:
        - VOSTFR
        - V O S T F R
        - V O S T FR
        - Sub FR
    headers:
      Cookie: "WebsiteID=********************"
    form:
      url: https://www.play-the.net/
      username: ****************
      password: ******************
      userfield: user
      passfield: pass
    rss: https://www.play-the.net/rss/dvdrip.rss
    preset: movies
  KAT_ROCK:
    email: # I don't want to receive email for this feed
      active: False
    private_torrents: no # and i don't want private torrent from this feed also
    rss: http://www.kat.ph/music/tag/rock/?rss=1
    preset: zik
  KAT_HEAVY_METAL:
    email:
      active: False
    private_torrents: no
    rss: http://www.kat.ph/music/tag/heavy-metal/?rss=1
    preset: zik
  KAT_METAL:
    email:
      active: False
    private_torrents: no
    rss: http://www.kat.ph/music/tag/metal/?rss=1
    preset: zik
  KAT_PROGRESSIVE_ROCK:
    email:
      active: False
    private_torrents: no
    rss: http://www.kat.ph/music/tag/progressive-rock/?rss=1
    preset: zik
  KAT_POWER_METAL:
    email:
      active: False
    private_torrents: no
    rss: http://www.kat.ph/music/tag/power-metal/?rss=1
    preset: zik
  KAT_MELODIC_METAL:
    email:
      active: False
    private_torrents: no
    rss: http://www.kat.ph/music/tag/melodic-metal/?rss=1
    preset: zik
  KAT_PROGRESSIVE_METAL:
    email:
      active: False
    private_torrents: no
    rss: http://www.kat.ph/music/tag/progressive-metal/?rss=1
    preset: zik
  KAT_SYMPHONIC_METAL:
    email:
      active: False
    private_torrents: no
    rss: http://www.kat.ph/music/tag/symphonic-metal/?rss=1
    preset: zik
  MONOVA_ROCK:
    email:
      active: False
    private_torrents: no
    rss: http://www.monova.org/rss.php?type=cat&id=54
    preset: zik
  MONOVA_METAL:
    email:
      active: False
    private_torrents: no
    rss: http://www.monova.org/rss.php?type=cat&id=52
    preset: zik
  METAL.IPLAY:
    email:
      active: False
    rss: http://metal.iplay.ro/rss.php?feed=dl&cat=63,74,41,75,53,2,52&passkey=***********************
    preset: zik
  MANUAL: # it's a feed that scan a dir for torrent, it's like the watch thing of deluge
# but this is better because flexget process the torrent, and then give it to deluge
# so the files get the preset TV and is processed. Of course i only put tv torrent here.
# torrents that flexget didn't catch, or new serie i found and have already some ep out.
    listdir: /home/seb/tor
    accept_all: yes
    manual: yes # need to use flexget --feed=MANUAL to use it
    preset: tv 
}}}
