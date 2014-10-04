'''UNNEFER'S ULTIMATE FLEXGET CONFIG'''
''Flexget (v1.2.149) + Transmission + File Renaming + Sorting + Cleaning + Email Notifications''

No more headaches trying to get Flexget to work and do the things you want it to - This config does the lot.

My config will do everything, it'll find what you want to download, rename the file when downloaded, move the file to a folder of your choice, clean all the leftover files and folder, and then email you to let you know what has been done.

Just follow the instructions included in the config and you're all set.

Enjoy :)

{{{
#########################################################################################################################################################################################
#                                                                                                                                                                                       #
# UNNEFER'S ULTIMATE FLEXGET CONFIG                                                                                                                                                     #
#                                                                                                                                                                                       #
# This config will automatically:                                                                                                                                                       #
#   Download episodes of your defined TV Series in 720p using EZTV and DRARBG                                                                                                           #
#   Send an email (via Gmail) to the defined Email address (from the defined Gmail address) to let you know the episode has been set to download                                        #
#   Match the downloaded file to TheTVDB and rename the file to the correct episode name                                                                                                #
#   Move the correctly named episode to your TV Series directory                                                                                                                        #
#   Send another email (via Gmail) to the defined Email address (from the defined Gmail address) to let you know the episode has been sorted                                            #
#   Download Movies in 1080p and using YIFY that are higher than the set IMDB rating                                                                                                    #
#   Send an email (via Gmail) to the defined Email address (from the defined Gmail address) to let you know the movie has been set to download                                          #
#   Match the downloaded file to IMDB and rename the file to the correct movie name                                                                                                     #
#   Move the correctly named movie to your Movies directory                                                                                                                             #
#   Send another email (via Gmail) to the defined Email address (from the defined Gmail address) to let you know the movie has been sorted                                              #
#                                                                                                                                                                                       #
# Settings you need to define in this config:                                                                                                                                           #
#   TMIPADDRESS = Transmission IP Address (ie. localhost)                                                                                                                               #
#   TMPORT = Transmission Port (ie. 9091)                                                                                                                                               #
#   TMUSERNAME = Transmission Username                                                                                                                                                  #
#   TMPASSWORD = Transmission Password                                                                                                                                                  #
#   GMAILFROMADDRESS = The Gmail address that emails will be sent from (needed to be able to send emails through Gmail's SMTP server)                                                   #
#   GMAILPASSWORD = The password of the Gmail address that emails will be sent from (needed to be able to send emails through Gmail's SMTP server)                                      #
#   EMAILTOADDRESS = The email address you want emails sent to                                                                                                                          #
#   TVSERIESNAME1 = A TV Series name (ie. Game of Thrones)                                                                                                                              #
#   TVSERIESNAME2 = Another TV Series name (ie. Gotham)                                                                                                                                 #
#   TVSERIESNAME3 = Another TV Series name (ie. Grimm)                                                                                                                                  #
#   TVSERIESNAME4 = Another TV Series name (ie. Z Nation)                                                                                                                               #
#   TVDIRECTORY = The directory where TV Series files are stored (ie. /storage/plexfiles/TV)                                                                                            #
#     Note: When you set the TVDIRECTORY, only edit the bit that says TVDIRECTORY - make sure to leave the rest of the location there to autogenerate and sort the TV Series correctly  #
#   MOVIEDOWNLOADLOCATION = The directory where Movie files will be downloaded (NOTHING ELSE CAN BE DOWNLOADED HERE - ie. /storage/transmission/Movies/)                                #
#   MOVIEDIRECTORY = The directory where Movie files are stored (ie. /storage/plexfiles/Movies)                                                                                         #
#   TVDOWNLOADLOCATION = The directory where TV Series files will be downloaded (NOTHING ELSE CAN BE DOWNLOADED HERE - ie. /storage/transmission/TV/)                                   #
#                                                                                                                                                                                       #
#########################################################################################################################################################################################
templates:
  global:
    regexp:
      reject:
        - WEB
        - WEB-DL

  transmissionrpc:
    transmission:
      host: TMIPADDRESS
      port: TMPORT
      username: TMUSERNAME
      password: TMPASSWORD
    clean_transmission:
      host: TMIPADDRESS
      port: TMPORT
      username: TMUSERNAME
      password: TMPASSWORD
      min_ratio: 0
      transmission_seed_limits: Yes
      enabled: Yes

  movies:
    imdb_required: yes
    quality: 1080p
    movie_queue: yes
    regexp:
      reject:
        - WEB
        - WEB-DL

  tv:
    thetvdb_lookup: yes
    quality: 720p
    regexp:
      reject:
        - WEB
        - WEB-DL
    series:
      group 1:      
        - TVSERIESNAME1
        - TVSERIESNAME2
        - TVSERIESNAME3
        - TVSERIESNAME4
tasks:
  Drarbg task:
    rss: http://rss.thepiratebay.se/user/a73c56ac59c186a918b8c882ace545b4
    priority: 1
    template: 
      - tv
      - transmissionrpc
    set:
      path: TVDOWNLOADLOCATION
    email:
      active: True
      from: GMAILFROMADDRESS
      to: EMAILTOADDRESS
      smtp_host: smtp.gmail.com
      smtp_port: 587
      smtp_username: GMAILFROMADDRESS
      smtp_password: GMAILPASSWORD
      smtp_tls: yes
      template: html-downloaded.template

  EZTV task:
    rss: http://ezrss.it/feed/
    priority: 2
    template: 
      - tv
      - transmissionrpc
    set:
      path: TVDOWNLOADLOCATION
    email:
      active: True
      from: GMAILFROMADDRESS
      to: EMAILTOADDRESS
      smtp_host: smtp.gmail.com
      smtp_port: 587
      smtp_username: GMAILFROMADDRESS
      smtp_password: GMAILPASSWORD
      smtp_tls: yes
      template: html-downloaded.template

  YIFY task:
    rss: http://yify-torrents.com/rss/0/All/All/0
    priority: 3
    content_size: 
      max: 2500
      min: 1000
    regexp:
      reject_excluding: 
        - YIFY
    queue_movies: yes
    template: 
      - movies
      - transmissionrpc
    imdb:
      min_year: 1980
      min_score: 5
    set:
      path: MOVIEDOWNLOADLOCATION
    email:
      active: True
      from: GMAILFROMADDRESS
      to: EMAILTOADDRESS
      smtp_host: smtp.gmail.com
      smtp_port: 587
      smtp_username: GMAILFROMADDRESS
      smtp_password: GMAILPASSWORD
      smtp_tls: yes
      template: html-downloaded.template

  sort-tvseries:
    find:
      path: TVDOWNLOADLOCATION
      regexp: '.*\.(mkv|mp4)$'
      recursive: yes
    seen: local
    template: tv
    series:
      settings:
        group 1:
          parse_only: yes
    regexp:
      reject: 
        - sample
    require_field: series_name
    accept_all: yes
    move:
      to: /TVDIRECTORY/{{series_name}}/{{series_name}} - Season {{series_season}}
      filename: '{{series_name}} - S{{series_season|pad(2)}}E{{series_episode|pad(2)}}'
      clean_source: 100
    email:
      active: True
      from: GMAILFROMADDRESS
      to: EMAILTOADDRESS
      smtp_host: smtp.gmail.com
      smtp_port: 587
      smtp_username: GMAILFROMADDRESS
      smtp_password: GMAILPASSWORD
      smtp_tls: yes
      template: html-moved.template

  sort-movies:
    find:
      path: MOVIEDOWNLOADLOCATION
      regexp: '.*\.(mkv|mp4)$'
      recursive: yes
    template: movies
    require_field: imdb_name
    accept_all: yes
    move:
      to: /MOVIEDIRECTORY/
      filename: '{{imdb_name}} ({{imdb_year}})'
      clean_source: 500
    email:
      active: True
      from: GMAILFROMADDRESS
      to: EMAILTOADDRESS
      smtp_host: smtp.gmail.com
      smtp_port: 587
      smtp_username: GMAILFROMADDRESS
      smtp_password: GMAILPASSWORD
      smtp_tls: yes
      template: html-moved.template
}}}