
{{{
feeds:
  nzbmatrix:
    rss: http://rss.nzbmatrix.com/rss.php?page=download&username=<username>&apikey=<your ip key>&subcat=42&english=1&ssl=1
    content_size: 
      max: 12000
      min: 1000
    quality: 720p
    imdb:
      min_score: 6.1
      min_votes: 4000
      min_year: 2009
      reject_genres:
        - musical
    imdb_required: yes
    exists_movie: K:\Movies
    imdb_rated: http://www.imdb.com/mymovies/list?l=XXXXXXX
    seen_movies: strict
    sabnzbd:
      key: <your sabnzbd api key>
      url: http://<your ip>/sabnzbd/api?
      category: movies
      username: <your username>
      password: <your password>

}}}
