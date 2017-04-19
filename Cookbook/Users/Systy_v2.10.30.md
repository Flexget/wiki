<code>


# Chargement des variables (comptes / mdp):
variables: secrets.yml

# Configuration de l'interface web - http://localhost:5050/ui + http://localhost:5050/api
web_server: 5050

# Création des templates
templates:
# Le template 'global' est appliqué à toutes les !!tasks!! sauf si 'template: no_global' déclaré
  global:
# Vérifie si 10Go d'espace libre sinon pas de téléchargement
    free_space:
      path: /home/downloader/DL/
      space: 10000
# Téléchargement des torrents avec le client transmission (http://www.transmissionbt.com/):
    transmission:
      host: localhost
      port: 9091
      username: '{? transmission.user ?}'
      password: '{? transmission.password ?}'
      main_file_only: yes
# 5 seeders minimum:
    torrent_alive: 
      min_seeds: 5
# Envoi d'un mail à la réussite d'une tache
    notify:
      entries:
        title: 'Notif Flexget'
        message: '{{title}}'
        via:
          - email:
              from: '{? google.email_2 ?}'
              to:
                - '{? google.email_1 ?}'
                - '{? google.email_2 ?}'
              smtp_host: smtp.gmail.com
              smtp_port: 587
              smtp_username: '{? google.email_2 ?}'
              smtp_password: '{? google.pass_email_2 ?}'
              smtp_tls: yes

# Fin du template 'global'

# Début des des templates "spécifiques"
  tv-global:
# Téléchargement des torrents series si taille entre 200Mo et 1200Mo
    content_size: 
      min: 150
      max: 1400
    download: /home/downloader/DL/WatchDir

  tv-my_shows_VOSTFR:
    configure_series:
# Attend 3 heures pour trouver la qualité demandé, sinon DL la meilleure qualité vue
      settings: 
        timeframe: 3 hours
        target: "<=720p h265|h264"
        identified_by: ep
      from:
# Séries ajoutées à la watchlist en fonction des fichiers déjà présents:
        filesystem: 
          path:
          - "/home/downloader/DL/Series/"
          recursive: True
# Séries ajoutées à la watchlist depuis une liste http://trakt.tv
        trakt_list: 
          username: '{? trakt.user ?}'
          strip_dates: yes
          list: series-list
          type: shows
# Ne pas téléchager les épisodes déja DL (téléchargement manuel)
    exists_series: 
      - "/home/downloader/DL/Series/"

    inputs:
      - discover:
          what:
# Chargement de la watchlist d'après "configure_series"
            - next_series_episodes: yes
                # from_start: yes
          from:
            # - cpasbien: # Recherche des torrents sur les trackers Cpasbien + T411
                # category: "series-vostfr"
            - t411:
                category: Série TV
                terms:
                  - VOSTFR
                max_results: 300
          release_estimations: ignore
    regexp:
# Rejete les torrents avec les mots suivants:
      reject: 
        - "complete"
        - "saison"

# On retrouve plus ou moins les mêmes éléments des séries
  movies-global: 
    content_size:
      min: 500
      max: 1500
    quality: "<=720p h264|h265"
    exists_movie:
      - "/home/downloader/DL/Movies/"
    seen_movies: strict # Don't download movies we've already seen
    regexp:
      reject:
        - "VOST"
        - "VFQ"
        - "VO"

# Ajout de films à la watchlist selon liste Trakt (https://trakt.tv)
  movies-queue-trakt: 
    inputs:
    - trakt_list:
        username: '{? trakt.user ?}'
        strip_dates: yes
        list: watchlist
        type: movies
    accept_all: yes
    list_add:
      - movie_list: list_trakt_movies
    no_entries_ok: yes

# Recherche des torrents ajoutés à la watchlist sur le tracker T411
  movies-DL-from-list: 
    discover:
      what:
        - movie_list: list_trakt_movies
      from:
        # - cpasbien:
            # category: "films-french"
        - t411:
            category: Film
            terms:
              - Français
            max_results: 200

  movies-t411:
    t411:
      category: Film
      terms:
        - Français
      max_results: 200

# Filtrage IMDB selon critères
    imdb: 
      min_score: 5.1 # +/- Decent movies 
      min_votes: 2000 # That people have actually watched
      min_year: 2005 # That are +/- new
      reject_genres:
        - musical
        - horror

  animation-t411:
    t411:
      category: Animation
      terms:
        - Français
      max_results: 200

# Filtrage IMDB selon critères
    imdb: 
      min_score: 5.1 # +/- Decent movies 
      min_votes: 2000 # That people have actually watched
      min_year: 2005 # That are +/- new
      reject_genres:
        - musical
        - horror

# Création des tâches (!!tasks!!)
tasks:
  DL_TV_Shows_VOSTFR:
# Classement / renomage des fichiers DL
    set: 
      path: /home/downloader/DL/Series/{{ series_name|replace('.',' ') }}/
      content_filename: "{{ series_name|replace(' ','.') }}.{{ series_id }}.VOSTFR.{{ quality|upper|replace(' ','.') }}{% if proper %}-proper{% endif %}"
    template:
      - tv-global
      - tv-my_shows_VOSTFR
    version_checker: yes
    priority: 10

  DL_Movies:
    set:
      path: /home/downloader/DL/Movies/
      content_filename: "{{ imdb_name|replace(' ','.') }}.{{ imdb_year }}-{{ quality|upper|replace(' ','.') }}"
    template:
      - movies-global
      - movies-t411
      - animation-t411
      - movies-DL-from-list
    priority: 20

  Movies_Queue_Trakt:
    template:
      - no_global
      - movies-queue-trakt
    priority: 30

# Modification de la planification par défaut des tâches
schedules:
  - tasks: ['DL_TV_Shows_VOSTFR', 'DL_Movies']
    interval:
      hours: 2

  - tasks: ['Movies_Queue_Trakt']  
    interval:
      hours: 6

</code>
