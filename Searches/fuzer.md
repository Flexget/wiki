# Fuzer
This search plugin will get results from Fuzer

## Configuration
Configuration requires rss_key, username, and password: (RSS key will be found in your Fuzer account preferences while username and password are your usual Fuzer login credentials.)
```
fuzer: 
  rss_key: xxxxxxxxxxxxxxxxxxxx
  username: xxxxxx
  password: xxxxxx
  category: HD Movies
```
`Category` option can be on or more of the following: `HD Movies`, `XviD`,`Israeli HD Movies` `BRRip`, `Israeli Movies`, `DVDR`, `Dubbed Movies`, `HD Shows`, `Shows`, `Israeli HD Shows`, `Israeli Shows`, `Dubbed Shows`, `Anime`, `Movie Packs`, `Shows Packs`.<BR>
It can also be any integer of any category that is or isn't list here.
 
Example:
```
fuzer: 
  rss_key: xxxxxxxxxxxxxxxxxxxx
  username: xxxxxx
  password: xxxxxx
  category:
    - HD Movies
    - 5 
    - Dubbed Movies
```