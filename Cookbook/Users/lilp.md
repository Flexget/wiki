Exemple de fichier de configuration pour le téléchargement des séries en VOSTFR et HD depuis T411 et avec le logiciel Deluged.
-Une partie VOSTFR/HD des séries pour récupérer les derniers épisodes.
-Une partie VOSTFR/HD des séries animés pour récupérer les derniers épisodes.
-Une partie VF/HD des séries animés pour récupérer les derniers épisodes.
-Une partie VOSTFR/HD des séries pour récupérer la série depuis l'épisode S01E01 (pour commencer une nouvelle série).

Chaque partie à son renommage de fichiers de la forme (NomSerie - SXXEXX - Qualité).
Chaque partie déplace les fichiers terminés dans un dossier de la forme (VotreChemin/NomSerie/SXX/).


Sample configuration file for downloading tvshows in HD VOSTFR since T411 and deluged with software.
-A Part VOSTFR / HD tvshows to get the latest episodes.
-A Part VOSTFR / HD animated tvshows to get the latest episodes.
-A Part VF / HD animated tvshows to get the latest episodes.
-A Part VOSTFR / HD tvshows to recover tvshows from episode S01E01 (to start a new series).

Each party to its renaming files of the form (TvShowsName - SXXEXX - Quality).
Each party moves files ending in a shape file (VotreChemin/TvShowsName/SXX/).


{{{
templates:
  t411:
    plugin_priority:
      headers: 250
    headers:
      User-Agent: "Mozilla/5.0 (X11; Ubuntu; Linux i686; rv:28.0) Gecko/20100101 Firefox/28.0"
      Accept: "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8"
      Accept-Charset: "ISO-8859-1,utf-8;q=0.7,*;q=0.3"
      Accept-Language: "fr-FR,fr;q=0.8,en-US;q=0.6,en;q=0.4"
      Cache-Control: "max-age=0"
      Connection: "keep-alive"
      Cookie: "uid=XxX; pass=XxX; authKey=XxX"

# DL des series VOSTFR en HD
  
  tv-my_shows:
    template:
      - t411
    series:
      - Your TvShow Name
    inputs:
      - html:
          url: "http://www.t411.io/torrents/search/?cat=210&subcat=433&term[17][]=721&term[7][]=16&term[7][]=15&term[7][]=1162&term[7][]=12&term[7][]=1174&term[7][]=1175&page={{i}}"
          increment: True
          title_from: title
          links_re:
          - "^http://www.t411.io/torrents/[^/]+(?!/)[^/]+$"
    deluge:
      content_filename: "{{series_name}} - {{series_id}} - {{quality}}"
      movedone: "/Your Destination Folder/{{ series_name }}/{{'S%02d'|format(series_season)}}"
      label: tv

# DL des serie animes en VF et en HD	  

  tv-my_shows_fr_anime:
    template:
      - t411
    series:
      - Your TvShow Name
    inputs:
      - html:
          url: "http://www.t411.io/torrents/search/&cat=210&subcat=637&term[17][]=541&term[7][]=16&term[7][]=15&term[7][]=1162&term[7][]=12&term[7][]=1174&term[7][]=1175&page={{i}}"
          increment: True
          title_from: title
          links_re:
          - "^http://www.t411.io/torrents/[^/]+(?!/)[^/]+$"


    deluge:
      content_filename: "{{series_name}} - {{series_id}} - {{quality}}"
      movedone: "/Your Destination Folder/{{ series_name }}/{{'S%02d'|format(series_season)}}"
      label: tv

# DL des series animes en VOSTFR et en HD

  tv-my_shows_anime:
    template:
      - t411
    series:
      - Your TvShow Name
    inputs:
      - html:
          url: "http://www.t411.io/torrents/search/?cat=210&subcat=637&term[17][]=721&term[7][]=16&term[7][]=15&term[7][]=1162&term[7][]=12&term[7][]=1174&term[7][]=1175&page={{i}}"
          increment: True
          title_from: title
          links_re:
          - "^http://www.t411.io/torrents/[^/]+(?!/)[^/]+$"
    deluge:
      content_filename: "{{series_name}} - {{series_id}} - {{quality}}"
      movedone: "/Your Destination Folder/{{ series_name }}/{{'S%02d'|format(series_season)}}"
      label: tv


#DL des series depuis le debut
  tvshows:
    regexp:
      reject_excluding:
        - VOSTFR

tasks:

#Taches Series VOSTFR et VF

  My_TV_Shows:
    priority: 1
    template:
      - tv-my_shows

  My_TV_Shows_fr_anime:
    priority: 3
    template:
      - tv-my_shows_fr_anime

  My_TV_Shows_anime:
    priority: 2
    template:
      - tv-my_shows_anime

#DL des series depuis le debut	  
  My-TV_Shows_debut:
    template: tvshows
    priority: 3
#    deluge: yes
    discover:
      what:
        - emit_series:
            from_start: yes
      from:
        - torrent411:
            username: XxX
            password: XxX
            category: Serie-TV
            sub_category: VOSTFR
    series:
      - Your TvShow Name:
          identified_by: ep
    deluge:
      content_filename: "{{series_name}} - {{series_id}} - {{quality}}"
      movedone: "/Your Destination Folder/{{ series_name }}/{{'S%02d'|format(series_season)}}"
      label: tva 
}}}

