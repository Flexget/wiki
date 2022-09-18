---
title: hyper_ch
description: 
published: true
date: 2022-09-18T05:23:06.865Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:23:04.183Z
---

This is the personal configuration of user hyper_ch.

This config consists of 5 main parts:

- global settings for all feeds in a preset
- a preset specifically aimed at tv shows
- a preset specifically aimed at movies in the movie queue
- a tv show feed section
- a movie feed section
- an external series.yml file that contains the list of followed tv shows

Some of the thoughts I put into it:

- The global setting for the preset exists to have the cookie file available all the times and also for filtering out some unwanted stuff. This is for me the same among tv shows and movies

- The reason for chosing to put the tv shows into a seperate file was to make the main config smaller and more readable.

- In the both sections I enforce a lq and hq size limit. That's to reflect "low quality" and "high quality". If there's a hq result found and within 2h not a lq result posted, then it'll use the hq result. I do this because I usually watch things once and then just delete stuff. No need to high quality.

- I also set no propers because often shows get replaced with a "clean" version. However most of the times those replacements don't make any sense or are a really minor improvement. If you just watch the show once, you don't need proper.

- The settings and group are necessary so that you can apply desired settings.

- only_new makes previous undecided entries to reject. I use this to speed up the lookups.

- the premiers are pretty much like the followed tv shows except I have flexget make a lookup on the genres. It will reject unwanted genres. Unfortunatley TVDB isn't that up-to-date on new shows, I hope TVRage will be added for lookup soon

- the movie_queue makes it use the movie queue

- the inputs in the feed section makes it also smaller. However there is one caveat. When you run flexget and check the log, then each feed will just be named as the main feed name e.g. "tvshows_feeds"

- the series.yml just contains the series and group tag and then the according entries

Also at the end you'll find a little movies.sh bash script which I use to add movies to the movie_queue from the shell.



```
##########################################################################################################################################################
#                                                                                                                                                        #
#                                                                                                                                                        #
#                                                        config.yml                                                                                      #
#                                                                                                                                                        #
#                                                                                                                                                        #
##########################################################################################################################################################

templates:
  global:
    cookies: ~/.flexget/cookies.sqlite
    regexp:
      reject:
        - french
        - german
        - dutch
        - ipod

  tv_common:
    inputs:
      - rss: https://www.rss1.com
      - rss: https://www.rss2.com
      - rss: http://www.rss3.com
    download: ~/rtorrent/Watch/
    exists_series:
      - ~/rtorrent/Completed/
      - ~/rtorrent/Downloads/
      - ~/rtorrent/Watch/
    interval: 5 minutes


  movies:
    inputs:
      - rss: http://www.rss4.com
      - rss: https://www.rss5.com
      - rss: http://www.rss6.com
      - rss: http://www.rss7.com
    content_size:
      max: 1700
    download: ~/rtorrent/Movies_Watch/
    exists_movie:
      - ~/rtorrent/Movies
      - ~/rtorrent/Downloads
      - ~/rtorrent/Movies_Watch
    quality:
      - <=1080p hdrip+
    movie_queue: yes
    proper_movies: no
    verify_ssl_certificates: no
    interval: 15 minutes

tasks:
  tv_feeds_lq:
    template: tv_common
    series:
      settings:
        group 1:
          propers: no
    content_size:
      max: 500
      strict: no
    include: series.yml

  tv_feeds_hq:
    template: tv_common
    series:
      settings:
        group 1:
          propers: no
    content_size:
      max: 1500
      strict: no
    delay: 2 hours
    include: series.yml

  premiers_lq:
    template: tv_common
    series_premiere:
      propers: no
      allow_seasonless: yes
    content_size:
      max: 500
      strict: no
    thetvdb_lookup: yes
    require_field: tvdb_genres
    regexp:
      reject:
        - documentary: {from: tvdb_genres}
        - talk show: {from: tvdb_genres}
        - game show: {from: tvdb_genres}
        - reality: {from: tvdb_genres}
        - news: {from: tvdb_genres}

  premiers_hq:
    template: tv_common
    series_premiere:
      propers: no
      allow_seasonless: yes
    content_size:
      max: 1500
      strict: no
    delay: 2 hours
    thetvdb_lookup: yes
    require_field: tvdb_genres
    regexp:
      reject:
        - documentary: {from: tvdb_genres}
        - talk show: {from: tvdb_genres}
        - game show: {from: tvdb_genres}
        - reality: {from: tvdb_genres}
        - news: {from: tvdb_genres}

  movie_feeds:
    template: movies

```




```
##########################################################################################################################################################
#                                                                                                                                                        #
#                                                                                                                                                        #
#                                                        series.yml                                                                                      #
#                                                                                                                                                        #
#                                                                                                                                                        #
##########################################################################################################################################################
series:
  group 1:
    - House
    - CSI Miami
    - CSI New York
    - CSI
    - NCIS Los Angeles
    - NCIS
    - Doctor Who 2005
    - Torchwood
    - The IT Crowd
    - The Big Bang Theory
    - Star Wars The Clone Wars
    - Fringe
    - Supernatural
    - [.... add more shows ....]
```




```/bin/bash
##########################################################################################################################################################
#                                                                                                                                                        #
#                                                                                                                                                        #
#                                                        movies.sh                                                                                       #
#                                                                                                                                                        #
#                                                                                                                                                        #
##########################################################################################################################################################


FLEXGET="/home/hyper/flexget-git/bin/flexget"           # Path to the flexget binary
QUALITY="ANY"

while [ -f "$CONFIG_LOCK" ] ;
do
        echo "Flexget is doing its run... waiting...."
        sleep 5
done


if [ -z "$1" ]; then
        echo "Add movies to queueu  ./movies IMDB_URL"
        echo "List movies in queue:";
        $FLEXGET --movie-queue list
        exit
fi

imdb1=${1##http*title}
imdb2=${imdb1//\//}

#$FLEXGET --movie-queue add $1 $QUALITY
echo "$FLEXGET movie-queue add imdb_id=${imdb2} $QUALITY"
$FLEXGET movie-queue add imdb_id=${imdb2} "${QUALITY}"
```