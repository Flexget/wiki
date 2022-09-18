---
title: lilp
description: 
published: true
date: 2022-09-18T05:23:14.753Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:23:12.104Z
---

Exemple de fichier de configuration pour le téléchargement des séries en VOSTFR et HD depuis T411, films avec IMDB en VOSTFR et HD avec le logiciel Deluged.
-Une partie Série TV qui récupère les séries en VOSTFR à partir du dernier épisode en date, ou depuis un épisode précis.
-Une partie Série Animation qui récupère les séries en VOSTFR depuis un épisode précis.
-Une partie Série Animation qui récupère les séries en VOSTFR à partir du dernier épisode en date.
-Une partie Films qui récupère la liste de notre Watchlist depuis IMDB puis fait une recherche en VOSTFR, 1080 ou 720.

Chaque partie à son renommage de fichiers de la forme (NomSerie - SXXEXX - Qualité).
Chaque partie déplace les fichiers terminés dans un dossier de la forme (VotreChemin/NomSerie/SXX/).
La partie film, déplace le fichiers téléchargé dans un dossier personnalisé.


Sample configuration file for downloading tvshows in HD VOSTFR since T411, movie with watchlist's IMDB in HD VOSTFR, deluged with software.
-A Part VOSTFR / HD tvshows to get the latest episodes.
-A Part VOSTFR / HD animated tvshows to get the latest episodes.
-A Part VF / HD animated tvshows to get the latest episodes.
-A Part VOSTFR / HD tvshows to recover tvshows from episode S01E01 (to start a new series).
-A Part Movie in VOSTFR/HD with watchlist's IMDB.

Each party to its renaming files of the form (TvShowsName - SXXEXX - Quality).
Each party moves files ending in a shape file (VotreChemin/TvShowsName/SXX/).
The movie part move the finish file in to a folder.

```
#Envois de mail lorsqu'un fichier est téléchargé
﻿email:
  from: xx.xx@gmail.com
  to:
   - xx.xx@gmail.com
  subject: Flexget
  smtp_host: smtp.gmail.com
  smtp_port: 587
  smtp_tls: yes
  smtp_username: xx.xx@gmail.com
  smtp_password: xx

templates:
  t411:
    plugin_priority:
      headers: 250

# DL des series VOSTFR en HD
  
  tv-my_shows:
    template:
      - t411
    series:
#Télécharge le dernier épisode de la série
      - Better Call Saul:
          identified_by: ep
      - Community:
          identified_by: ep
#Télécharge à partir de l'épisode S06E10
      - Cougar Town:
          begin: S06E10
      - Brooklyn Nine-Nine:
          identified_by: ep
      - Fear The Walking Dead:
          identified_by: ep
      - Game Of Thrones:
          identified_by: ep
      - House Of Cards:
          begin: S03E13
      - Homeland:
          identified_by: ep
      - Its Always Sunny In Philadelphia:
          begin: S09E10
      - Limitless:
          identified_by: ep
      - Mad Men:
          identified_by: ep
      - Modern Family:
          identified_by: ep
      - Mr. Robot:
          identified_by: ep
      - Orange Is The New Black:
          identified_by: ep
      - Parks And Recreation:
          begin: S07E12
      - Silicon valley:
          identified_by: ep
      - The Aliens:
          begin: S01E01
      - The Americans:
          identified_by: ep
      - The Big Bang Theory:
          identified_by: ep
      - The Last Man On Earth:
          identified_by: ep
      - The Walking Dead:
          identified_by: ep
      - True Detective:
          identified_by: ep
      - Two And A Half Men:
            begin: S12E14
      - Workaholics:
          begin: S05E01
      - Vikings:
          begin: S03E10
      - The X-Files:
          identified_by: ep
#Envois le fichiers torrent à deluge et renomme le fichier une fois téléchargé de la forme The Simpsons - S20E15 - 720p.avi et déplace le fichier dans le dossier /Series/NomDeLaSerie/S**
    deluge:
      content_filename: "{{series_name}} - {{series_id}} - {{quality}}"
      movedone: "/Series/{{ series_name }}/{{'S%02d'|format(series_season)}}"
      label: tv
#Reject les torrent comportant les mots x265 et h265
    regexp:
      reject:
        - x265
        - h265

# DL des serie animes en VF et en HD

  tv-my_shows_fr_anime:
    template:
      - t411
    series:
      - Simpson:
#          identified_by: ep
           begin: S27E15
    deluge:
      content_filename: "{{series_name}} - {{series_id}} - {{quality}}"
      movedone: "/Series/{{ series_name }}/{{'S%02d'|format(series_season)}}"
      label: tv
    regexp:
      reject:
        - x265
        - h265


# DL des series animes en VOSTFR et en HD

  tv-my_shows_anime:
    template:
      - t411
    series:
      - American Dad:
          identified_by: ep
      - Family Guy:
          identified_by: ep
      - Futurama:
          identified_by: ep
      - South Park:
          identified_by: ep
      - The Simpsons:
          identified_by: ep
      - Bojack Horseman:
          identified_by: ep
    deluge:
      content_filename: "{{series_name}} - {{series_id}} - {{quality}}"
      movedone: "/Series/{{ series_name }}/{{'S%02d'|format(series_season)}}"
      label: tv
    regexp:
      reject:
        - x265
        - h265

tasks:

#Taches Series VOSTFR et VF

  My_TV_Shows:
    priority: 1
    template:
      - tv-my_shows
    discover:
      what:
        - emit_series: yes
#Utilise l'api T411 en allant chercher dans la catégorie Série TV, puis dans les sous-catégorie VOSTFR et TVripHD 1080 et TVripHD720
      from:
        - t411:
            category: Série TV
            terms:
              - VOSTFR
              - TVripHD 1080
              - TVripHD 720

  
  My_TV_Shows_fr_anime:
    priority: 2
    template:
      - tv-my_shows_fr_anime
    discover:
      what:
        - emit_series: yes
      from:
        - t411:
            category: Animation Série
            terms:
              - Français
              - TVripHD 1080
              - TVripHD 720

  My_TV_Shows_anime:
    priority: 3
    template:
      - tv-my_shows_anime
    discover:
      what:
        - emit_series: yes
      from:
        - t411:
            category: Animation Série
            terms:
              - VOSTFR
              - TVripHD 1080
              - TVripHD 720

#Télécharge et déplace les films dans le dossier /Films
  movie_vo:
    deluge:
      movedone: "/Films/"
      label: movies
#Rejete les torrents comportant les mots x265 et h265
    regexp:
      reject:
        - x265
        - h265
#Récupère la liste des films depuis la Watchlist d'IMDB de l'utilisateur ur****
    discover:
      what:
        - imdb_list:
            list: watchlist
            user_id: urxxxx
#Effectue une recherche sur T411 dans la catégorie FIlms avec la qualité VOSTFR, HDrip 1080 et HDrip 720
      from:
        - t411:
            category: Films
            terms:
              - VOSTFR
              - HDrip 1080
              - HDrip 720
```


PS : Je tiens à remercier olygraph2, lildadou3 et jonybat pour leurs aides
I want to thank olygraph2, lildadou3 and jonybat for their help
