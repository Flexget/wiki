Hors_Sujet  

A la base je ne sais pas programmer, mais utilisant Flexget depuis quelques temps, il a bien fallu s'y mettre doucement.
J'ai essayer d'organiser au plus clair (pour moi) mes templates / tasks, mais ma logique n'est sans doute pas celle des autres ;)
Je vous présente néanmoins mon fichier de configuration qui pourra sans doute aider des débutants, comme j'ai pu moi-même être grandement aidé par les exemples des autres. D'ailleurs, un GRAND merci à Lildadou !!!  

/Hors_Sujet


Fichier de configuration pour le téléchargement (commentaires sont présents dans le code pour plus de détails):
- De séries en VOSTFR (h264/h265) depuis fichiers existants + liste fixe + liste Trakt
- De films en français depuis liste dynamique IMDB + liste Trakt
Téléchargement sur les trackers T411 (dernier plugin n'est pas intégré officiellement au 16.02.2016) + Cpasbien.
Un peu de renommage de fichier.
Le tout téléchargés avec le logiciel de torrent Transmission.

----

Off_Topic  

Basically I can not program, but using Flexget for some time, it was necessary to put it gently.
I try to organize more clear (for me) my templates / tasks, but my logic is probably not that of others ;)
Nevertheless, I present my configuration file that will probably help beginners, as I myself have been greatly helped by the examples of others. Moreover, a BIG thank you to Lildadou !!!  

/Off_Topic


Configuration file for download (comments are present in the code for details / sorry it's french comments only):
- From series VOSTFR (H264 / H265) from existing files + fixed list + Trakt list
- From French movies from IMDB dynamic list + list Trakt
Download trackers T411 (the last plugin is not officially integrated 02/16/2016) + Cpasbien.
Some file renaming.
All downloaded with the Transmission torrent software.

{{{
# Configuration de l'interface web - http://localhost:5050/ui + http://localhost:5050/api
web_server:
  bind: 0.0.0.0
  port: 5050
api: yes
webui: yes

# Création des templates
templates:
# Le template 'global' est appliqué à toutes les 'tasks' sauf si 'template: no_global' déclaré
  global:
    email: # Envoi d'un mail à la réussite ou échec d'une tache (task)
      active: True
      from: FlexGet
      to:
        - blabla@gmail.com
        - blabla1@gmail.com
      smtp_host: smtp.gmail.com
      smtp_port: 587
      smtp_username: blabla@gmail.com
      smtp_password: My_pass
      smtp_tls: yes
      template: default
    free_space: # Vérifie si 20Go d'espace libre sinon pas de téléchargement
      path: /home/downloader/DL/
      space: 20000
    transmission: # Téléchargement des torrents avec le client transmission (http://www.transmissionbt.com/)
      host: localhost
      port: 9091
      username: My_username
      password: My_password
      main_file_only: yes # téléchargement du fichier principal du torrent
    torrent_alive: # 5 seeders minimum
      min_seeds: 5
# Fin du template 'global' 

# Début des des templates "spécifiques"
  tv-global: 
    content_size: # Téléchargement des torrents series si taille entre 200Mo et 1200Mo (1,2Go)
      min: 150
      max: 1200
    download: /home/downloader/DL/WatchDir

  tv-my_shows_VOSTFR:
    configure_series:
      settings: # Attend 6 heures pour cette qualité sinon DL la meilleure qualité vue
        timeframe: 6 hours
        target: "<=720p h264|h265"
      from:
        filesystem: # Séries ajoutées à la watchlist en fonction des fichiers déjà présents
          path:
          - "/home/downloader/DL/Series/"
          recursive: True
        trakt_list: # Séries ajoutées à la watchlist depuis une liste http://trakt.tv
          username: systy
          strip_dates: yes
          list: series-list
          type: shows
    exists_series: # Ne pas téléchager les épisodes déja DL (téléchargement manuel)
      - "/home/downloader/DL/Series/"
    series: # Séries ajoutées à la watchlist si présentes dans la liste
      settings:
        group_1: # Attend 6 heures pour cette qualité sinon DL la meilleure qualité vue
          timeframe: 6 hours
          target: "<=720p h264|h265"
          identified_by: ep
      group_1:
        - Homeland
        - House of Cards
        - Game of Thrones
        - Under the Dome
        - Person of Interest
        - Royal Pains
        - Rectify
        - The Originals
        - Arrow
        - Masters of Sex
        - The Vampire Diaries
        - The 100
        - Better Call Saul
        - The Flash
        - Jessica Jones
        - Agent Carter
        - The Expanse
        - Legends of Tomorrow
        - Gotham
    inputs:
      - discover:
          what:
            - emit_series: # Chargement de la watchlist
                from_start: yes
          from:
            - cpasbien: # Recherche des torrents sur les trackers Cpasbien + T411
                category: "series-vostfr"
            - t411:
                category: "Série TV"
                terms:
                  - VOSTFR
                max_results: 300
          ignore_estimations: yes
    regexp:
      reject: # Rejete les torrents avec les mots suivants:
        - "complete"
        - "saison"

  movies-global: # On retrouve plus ou moins les mêmes éléments pour les séries
    content_size:
      min: 500
      max: 1500
    quality: divx|xvid # Pas de h264|h265, mon Raspberry/Kodi n'aime pas ;)
    exists_movie:
      - "/home/downloader/DL/Movies/"
    seen_movies: strict # Don't download movies we've already seen
    regexp:
      reject:
        - "VOST"
        - "VFQ"
        - "VO"
    imdb_required: yes # Doit être trouvé sur IMDB (https://www.imdb.com)
    imdb: # Filtrage IMDB selon critères
      min_score: 5.1 # +/- Decent movies 
      min_votes: 2000 # That people have actually watched
      min_year: 2005 # That are +/- new
      reject_genres:
        - musical
        - horror

  movies-queue-trakt: # Ajout de films à la watchlist selon liste Trakt (https://trakt.tv)
    inputs:
    - trakt_list:
        username: systy
        strip_dates: yes
        list: watchlist
        type: movies
    accept_all: yes
    movie_queue: add    
    no_entries_ok: yes

  movies-queue-dynamic-imdb:  # Ajout de films à la watchlist selon liste dynamique IMDB (https://trakt.tv)
    inputs:
    - dynamic_imdb:
        id: 
          - nm0000197 # Jack Nicholson
          - nm0000134 # Robert De Niro
          - nm0000158 # Tom Hanks
          - nm0000093 # Brad Pitt
          - nm0000164 # Anthony Hopkins 
          - nm0000243 # Denzel Washington
          - nm0000432 # Gene Hackman
          - nm0000142 # Clint Eastwood
          - nm0000138 # Leonardo DiCaprio
          - nm0000168 # Samuel L. Jackson
          - nm0000169 # Tommy Lee Jones
          - nm0000115 # Nicolas Cage
          - nm0000151 # Morgan Freeman 
          - nm0000128 # Russell Crowe
          - nm0000246 # Bruce Willis
          - nm0000136 # Johnny Depp
          - nm0000129 # Tom Cruise
          - nm0000288 # Christian Bale
          - nm0000123 # George Clooney
          - nm0000125 # Sean Connery
          - nm0000148 # Harrison Ford 
          - nm0000354 # Matt Damon
          - nm0000140 # Michael Douglas 
          - nm0001845 # Forest Whitaker
          - nm0000553 # Liam Neeson
          - nm0000226 # Will Smith 
          - nm0000206 # Keanu Reeves
          - nm0009190 # J.J. Abrams 
          - nm0000217 # Martin Scorsese
          - nm0000184 # George Lucas 
          - nm0000233 # Quentin Tarantino
          - nm0000229 # Steven Spielberg
          - nm0000116 # James Cameron 
          - nm0000318 # Tim Burton
        max_entries: 1000
    imdb_required: yes
    imdb:
      min_score: 5.1 # +/- Decent movies 
      min_votes: 2000 # That people have actually watched
      min_year: 2005 # That are +/- new
      reject_genres:
        - musical
        - horror
    accept_all: yes
    movie_queue: add    
    no_entries_ok: yes

  movies-queued: # Recherche des torrents ajoutés à la watchlist sur les trackers Cpasbien + T411
    movie_queue: accept
    discover:
      what:
        - emit_movie_queue: yes
      from:
        - cpasbien:
            category: "films-french"
        - t411:
            category: "Film"
            terms:
              - Français
            max_results: 200

# Création des tâches (tasks)
tasks:
  TV_Shows_VOSTFR:
    set: # Classement / renomage des fichiers DL
      path: /home/downloader/DL/Series/{{ series_name|replace('.',' ') }}/
      content_filename: "{{ series_name|replace(' ','.') }}.{{ series_id }}.VOSTFR.{{ quality|upper|replace(' ','.') }}{% if proper %}-proper{% endif %}"
    template:
      - tv-global
      - tv-my_shows_VOSTFR
    version_checker: yes
    priority: 10

  Movies_Queue_Trakt:
    template:
      - no_global
      - movies-queue-trakt
    priority: 20

  Movies_Queue_Imdb:
    template:
      - no_global
      - movies-queue-dynamic-imdb
    priority: 30

  My_Movies:
    set:
      path: /home/downloader/DL/Movies/
      content_filename: "{{ imdb_name|replace(' ','.') }}-{{ imdb_year }}-{{ quality|replace(' ','.') upper }}"
    template:
      - movies-global
      - movies-queued
    priority: 40


# Modification de la planification par défaut des tâches
schedules:
  - tasks: TV_Shows_VOSTFR
    interval:
      hours: 2
  - tasks: Movies_Queue_Trakt
    interval:
      hours: 2
  - tasks: Movies_Queue_Imdb
    interval:
      days: 7
  - tasks: My_Movies
    interval:
      days: 1}}}