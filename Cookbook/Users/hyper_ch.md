This is the personal configuration of user hyper_ch.

This config concists of 6 main parts:

- global settings for all feeds in a preset
- a preset specifically aimed at watched shows
- a preset specifically aimed at tv premiers
- a preset specifically aimed at movies in the movie queue
- a tv show feed section
- a movie feed section
- an external series.yml file that contains the list of followed tv shows

Some of the thoughts I put into it:

- The global setting for the preset exists to have the cookie file available all the times and also for filtering out some unwanted stuff. This is for me the same among tv shows and movies

- The reason for chosing to put the followed tv shows into a seperate file was to make the main config smaller and more viewable.
- In the tv section I did set a max. file size of 800MB. Mainly because I prefer xvid as I just watch a show usually once. And if there is a double episode, it should be around 700MB. So 800MB is a save margin.
- I also set no propers because often shows get replaced with a "clean" version. Hoever most of the times those replacements don't make any sense or are a really minor improvement. If you just watch the show once, you don't need proper.
- The settings and group are necessary so taht you can apply desired settings.
- only_new makes previous undecided entries to reject. I use this to speed up the lookups.
- the premiers are pretty much like the followed tv shows except I have flexget make a lookup on the genres. It will reject unwanted genres. Unfortunatley TMDB isn't that up-to-date on new shows, I hope TVRage will be added for lookup soon

- I also watch movies hardly more than once. For that reason I also apply file size limit and quality limits
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
#    accept:
#      - S01E01
    reject:
       - french
       - german
       - dutch
       - ipod

  tv:
    content_size:
      max: 800
    download: ~/rtorrent/Watch/
    exists_series:
      - ~/rtorrent/Completed/
      - ~/rtorrent/Downloads/
      - ~/rtorrent/Watch/
    series:
      settings:
        group 1:
          propers: no
          max_quality: bdrip
    include: series.yml
    only_new: yes

 prems:
    content_size:
      max: 800
    download: ~/rtorrent/Watch/
    exists_series:
      - ~/rtorrent/Completed/
      - ~/rtorrent/Downloads/
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
    only_new: yes

  movies:
    content_size:
      max: 1700
    download: ~/rtorrent/Movies_Watch/
    quality:
      min: hdtv
      max: bdrip
    movie_queue: yes
    proper_movies: no
    only_new: yes



feeds:
  tvshows_feeds:
    inputs:
      - rss: http://www.TVtracker1.com/rss.php
      - rss: http://www.TVtracker2.com/rss.php
      - rss: http://www.TVtracker3.com/rss.php
    preset:
      - tv
      - prems
    interval: 5 minutes

  movie_feeds:
    inputs:
      - rss: http://www.MOVIEtracker1.com/rss.php
      - rss: http://www.MOVIEtracker2.com/rss.php
      - rss: http://www.MOVIEtracker3.com/rss.php
    preset:
      - movies
    interval: 15 minutes

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
##########################################################################################################################################################
#                                                                                                                                                        #
#                                                                                                                                                        #
#                                                        movies.sh                                                                                       #
#                                                                                                                                                        #
#                                                                                                                                                        #
##########################################################################################################################################################
#!/bin/bash

FLEXGET="~/flexget-svn/bin/flexget"                     # Path to the flexget binary
QUALITY="ANY"                                           # Set quality to any as flexget will do it with min/max quality
CONFIG_LOCK="~/.flexget/.config-lock"                   # Set config lock file for flexget
FORCE="False"                                           # Set True or False

while [ -f "$CONFIG_LOCK" ] ;
do
        echo "Flexget is doing its run... waiting...."
        sleep 5
done


if [ -z "$1" ]; then
        echo "Add movies to queueu  ./movies.sh IMDB_URL  or  ./movies.sh TMDB_ID"
        echo "List movies in queue:";
        $FLEXGET --movie-queue list
        exit
fi

$FLEXGET --movie-queue add $1 $QUALITY $FORCE
}}}