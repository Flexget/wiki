---
title: lostfilm
description: 
published: true
date: 2022-09-18T04:52:52.149Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:52:48.454Z
---

[bash]
schedules:

  # Run every task once an hour

  - tasks: '*'

    interval:

      minutes: 30

templates:

  global:

    transmission:

      host: 127.0.0.1

      port: 9091

      username: 'pi'

      password: '110778'

    set:

      path: '/mnt/tm/media/nfsi/{{series_name}}/Season {{series_season}}/'

  telega:

    notify:

       entries:

          title: FlexGet Notification

          message: |+

             {%if task in ["retreive_from_couchpotato","dynamic_imdb_actors"]%}*New movie added to queue*

             {%else%}*Download Started from task:* {{task|replace("_", "-")}}

             {%endif%}

             {% if series_name is defined -%}

             *{{series_name}}* - {{series_id}} - {{quality|d('')}}

             *{{tvmaze_episode_name|d(tvdb_ep_name)|d('')}}*

             [Image]({{tvmaze_series_original_image|replace("_", "%5F")}})

             [Show page]({{tvmaze_series_url|replace("_", "%5F")}})

             {% elif imdb_name is defined -%}

             *{{imdb_name}}* - ({{imdb_year}})

             {{quality|d('')}}

             {{imdb_score}}/10 - {{imdb_votes}} votes

             {{imdb_genres|join(', ')|title}}

             *Plot:* {{imdb_plot_outline}}

             [Image]({{tmdb_posters[0]|replace("_", "%5F")}})

             [Movie Page]({{imdb_url|d('')}})

             {% else -%}

             {{title}}

             {%- endif -%}

          via:

            - telegram:

                bot_token: "2036251468:AAEJuhtCk77J7wNvqw4QR3gefx4x4MIocy0"

                parse_mode: markdown

                recipients:

                   - username: 'emil110'

                   - group: ''



#tasks:

 # rutracker.org: in progress

 #   template:

 #       - tvshows

 #   rutracker_auth:

 #       username: '**********'

 #       password: '***********'

 #   urlrewrite:

 #       rutracker:

 #       regexp: '^(?Pd+)&amp;amp;amp;amp;amp;amp;amp;lt;/pre&amp;amp;amp;amp;amp;amp;amp;gt;

&amp;amp;amp;amp;amp;amp;amp;lt;pre class="wp-block-syntaxhighlighter-code"&amp;amp;amp;amp;amp;amp;amp;gt; #       format: 'http://rutracker.org/forum/viewtopic.php?t=g'

  LostFilm:

    headers:

      cookie: 'uid=4774388;usess=emil110'

    rss:

      url: 'http://retre.org/rssdd.xml'

      ascii: yes

    tvmaze_lookup: yes

    template:

      - global

      - telega

      - sendtomail

      - discord

    regexp:

      reject:

        - E99

    quality: 720p+

    manipulate:

      - title:

          replace:

            regexp: '(.*)((.+)).(.*)s((.+))s[(.+)]'

            format: '2.4.5'

      - title:

          replace:

            regexp: '(.*).MP4'

            format: '1.720p'

      - title:

          replace:

            regexp: '(.*).SD'

            format: '1.480p'

    series:

     720p:

      - The Rookie

      - Project Blue Book

      - Whiskey Cavalier

      - The Expanse

      - The Good Doctor

      - Lethal Weapon

      - Better Call Saul:

          path: '/mnt/tm/media/seasons/{{series_name}}/Season {{series_season}}/'

      - Game of Thrones:

          path: '/mnt/tm/media/seasons/Game of Thrones {{series_season}} - LostFilm.TV [MP4]/'

      - Lucifer:

           path: '/mnt/tm/media/seasons/Lucifer {{series_season}} - LostFilm.TV [MP4]/'

     1080p:

      - The Orville:

           path: '/mnt/tm/media/nfsi/{{series_name}}/Season {{series_season}}/'

      - Happy!

[/bash]