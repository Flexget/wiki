### New movies plugin
```
movies:
  comedy, scifi:
    imdb_score: 6.2+
    imdb_year: 1992+
    imdb_votes: 5000+
  horror:
    imdb_year: 1980-1990
    action: accept # implicit
  musical:
    action: reject # explicit

# how to handle actor accepts?
	
  actor[jackie, chan]:
    action: accept
    
# what about musical with jackie chan?

# languages? primary language?
# "hated" actors?
```
