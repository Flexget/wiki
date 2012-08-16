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

- In the tv section I did set a max. file size of 800MB. Mainly because I prefer xvid as I just watch a show usually once. And if there is a double episode, it should be around 700MB. So 800MB is a save margin.

- I also set no propers because often shows get replaced with a "clean" version. Hoever most of the times those replacements don't make any sense or are a really minor improvement. If you just watch the show once, you don't need proper.

- The settings and group are necessary so that you can apply desired settings.

- only_new makes previous undecided entries to reject. I use this to speed up the lookups.

- the premiers are pretty much like the followed tv shows except I have flexget make a lookup on the genres. It will reject unwanted genres. Unfortunatley TMDB isn't that up-to-date on new shows, I hope TVRage will be added for lookup soon

- the movie_queue makes it use the movie queue

- the inputs in the feed section makes it also smaller. However there is one caveat. When you run flexget and check the log, then each feed will just be named as the main feed name e.g. "tvshows_feeds"

- the series.yml just contains the series and group tag and then the according entries

Also at the end you'll find a little movies.sh bash script which I use to add movies to the movie_queue from the shell.



{{{
##########################################################################################################################################################
#                                                                                                                                                        #
#                                                                                                                                                        #
#                                                        config.yml                                                                                      #
#                                                                                                                                                        #
#                                                                                                                                                        #
##########################################################################################################################################################

presets:
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
      - rss: http://www.tv-feed1.com/rss.php
      - rss: http://www.tv-feed2.com/rss.php
      - rss: http://www.tv-feed3.com/rss.php
    content_size:
      max: 800
    download: ~/rtorrent/Watch/
    quality: "<=1080p r5+"
    exists_series:
      - ~/rtorrent/Completed/
      - ~/rtorrent/Downloads/
      - ~/rtorrent/Watch/
    interval: 5 minutes


  movies:
    inputs:
      - rss: http://www.movie-feed1.com/rss.php
      - rss: http://www.movie-feed2.com/rss.php
      - rss: http://www.movie-feed3.com/rss.php
    content_size:
      max: 1700
    download: ~/rtorrent/Movies_Watch/
    exists_movie:
      - ~/rtorrent/Movies
      - ~/rtorrent/Downloads
      - ~/rtorrent/Movies_Watch
    quality: "<=1080p r5+"
    movie_queue: yes
    proper_movies: no
    verify_ssl_certificates: no
    interval: 15 minutes

tasks:
  tv_feeds:
    preset: tv_common
    series:
      settings:
        group 1:
          propers: no
    include: series.yml

  premiers:
    preset: tv_common
    series_premiere:
      propers: no
    thetvdb_lookup: yes
    if:
      - not has_field('series_genres'): reject
      - series_id == 'S01E01':  
          regexp:
            reject:
              - documentary
              - talk show
              - game show
              - reality
              - news
            from: series_genres

  movie_feeds:
    preset: movies


}}}




{{{
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
}}}




{{{
#!/bin/bash
##########################################################################################################################################################
#                                                                                                                                                        #
#                                                                                                                                                        #
#                                                        movies.sh                                                                                       #
#                                                                                                                                                        #
#                                                                                                                                                        #
##########################################################################################################################################################

#!/bin/bash

FLEXGET="/home/hyper/flexget-svn/bin/flexget"           # Path to the flexget binary
QUALITY="hdtv 360p 480p web-dl dvdrip bdrip hr"         # Set desired qualities
QUALITY="ANY"
QUALITY="<=720p r5+"
CONFIG_LOCK="/home/hyper/.flexget/.config-lock"         # Set config lock file for flexget
FORCE="False"                                           # Set True or False

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

$FLEXGET --movie-queue add imdb_id=${imdb2} "${QUALITY}" ${FORCE}
}}}