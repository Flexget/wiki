== Input: NZBMatrix RSS Feed ==
This starts with an RSS feed from [http://nzbmatrix.com NZBMatrix], which requires a VIP account with them. In this case, I am pulling all english HD x264 encoded movies. You can create your own [http://rss.nzbmatrix.com/ personalized RSS feed] for other categories as well. 

== Filters: ==
content_size: is probably not needed, but can be used to filter things that are obviously too big or small. 
quality: allows controls what quality of movie you want. Here I indicate 720p.
imdb: allows many methods to filter based on IMDB such as average rating, number of ratings, as well as rejecting genres of movies you don't like.
imdb_required: ensures that the movie must have an imdb link
exists_movie: Checks to see if you already have a copy of it downloaded on local storage. If so, then it doesn't pass any further. 
imdb_rated: allows you to reject movies that you have already voted on at IMDB (and thus probably already watched)
seen_movies: rejects movies that have already been downloaded but might be from a different group/release

== Download: SABnzbd ==
Finally any movies that make it through all filtering is then downloaded with SABnzbd. key and url are needed whereas the other fields are optional based on your set up. 

Interesting option would be to instead output to your own RSS feed, which many sabnzbd servers could then use to automatically download from. You could create a Bob's top horror movies list that your friends/family could subscribe to. 

==config.yml==

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
