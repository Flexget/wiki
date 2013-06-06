This is the personal configuration of user foulou . I will try to remember to update this page when I make changes.

Updated Config if this one is outdated : http://pastebin.com/CsSLVCJA


{{{
presets:
  global:
    make_rss: /var/www/rss/flexget.rss
    email:
      from: xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
      to:
        - xxxxxxxxxxxxxxxxxxxxxxxxx
        - xxxxxxxxxxxxxxxxxxxxxxxxx
      smtp_host: localhost
      smtp_port: 25
    deluge:
      queuetotop: yes
      user: xxxxxxx
      pass: xxxxxxx
  ftdb_cookie:
    verify_ssl_certificates: no
    headers:
      Cookie: "WebsiteID=xxxxxxxxxxxxxxxxx"
      User-Agent: "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/535.1 (KHTML, like Gecko) Chrome/14.0.835.202 Safari/535.1"
  zik:
    deluge:
      ratio: 1000
      removeatratio: yes
    content_filter:
      require:
        - '*.flac'
    include : ziklist.yml
    set:
      path: /home/seb/media/Downloads/Torrent/Downloading/
      movedone: "/home/seb/media/HDD2_1To/Musique_DL"
      label: Zik
  tv:
    regexp:
      from: title
      reject:
        - MiND
        - SSL
    content_filter:
      require:
        - '*.avi'
        - '*.mkv'
        - '*.mp4'
    import_series:
      from:
        inputs:
          - trakt_list:
              username: foulou
              api_key: xxxxxxxxxxxxxxxxxxx
              series: watchlist
          - trakt_list:
              username: foulou
              api_key: xxxxxxxxxxxxxxxxxxx
              series: all
      settings:
        quality: HDTV
    series:
      settings:
        HDTV:
          propers: yes
          qualities:
            - hdtv <720p h264|xvid
    thetvdb_lookup: yes
    set:
      path: /home/seb/media/Downloads/Torrent/Downloading/
      movedone: "/home/seb/media/Series/{{ tvdb_series_name }}/Season 0{{ tvdb_season }}"
      label: TV
    exists_series:
      - /home/seb/media/Series
      - "/home/seb/media/HDD2_1To/Series Ended"
  animes:
    content_filter:
      require:
        - '*.avi'
        - '*.mkv'
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
      path: /home/seb/media/Downloads/Torrent/Downloading/
      movedone: "/home/seb/media/HDD2_1To/Animes/{{ tvdb_series_name }}/Season {{ tvdb_season }}"
      label: Animes
      main_file_only: yes
      content_filename: "{{ tvdb_series_name }}.{{ tvdb_ep_id }} - ({{ tvdb_absolute_number }})"
    exists_series:
      - /home/seb/media/HDD2_1To/Animes
  movies:
    content_filter:
      require:
        - '*.avi'
        - '*.mkv'
        - '*.mp4'
    imdb_required: yes
    imdb:
      min_year: 2011
      reject_genres:
        - News
        - Documentary
    quality:
      - dvdrip
      - bluray
    content_size:
      max: 1600
      min: 650
    seen_movies: strict
    exists_movie:
      - "/home/seb/media/Movies/"
      - "/home/seb/media/FILMS_OLD/"
    imdb_lookup: yes
    set:
      label: Movies
      path: /home/seb/media/Downloads/Torrent/Downloading
      movedone: "/home/seb/media/Movies/"
tasks:
  FTDB_TV:
    rss: http://www.frenchtorrentdb.com/rss/xxxxxxxxxxxxxxxxxxxxx/tv_vostfr.rss
    preset:
      - tv
      - ftdb_cookie
  FTDB_DVDRIP:
    regexp:
      from: title
      reject:
        - VOSTFR
        - V O S T F R
        - V O S T FR
        - Sub FR
    rss: http://www.frenchtorrentdb.com/rss/xxxxxxxxxxxxxxxxxxxxx/dvdrip.rss
    preset:
      - movies
      - ftdb_cookie
  ADDSERIE:
    listdir: /home/seb/tor/series
    accept_all: yes
    manual: yes
    preset: tv
  ADDMOVIE:
    listdir: /home/seb/tor/movies
    accept_all: yes
    manual: yes
    preset: movies
  ADDSPECTACLE:
    listdir: /home/seb/tor/spectacles
    accept_all: yes
    manual: yes
    preset: spectacles
  ADDZIK:
    listdir: /home/seb/tor/zik
    accept_all: yes
    manual: yes
    preset: zik
  ADDEBOOK:
    listdir: /home/seb/tor/ebook
    accept_all: yes
    manual: yes
    preset: ebook
  ADDANIME:
    listdir: /home/seb/tor/animes
    accept_all: yes
    manual: yes
    preset: animes
}}}