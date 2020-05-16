# FileList w/ API
This search plugin will get results from [FileList](https://filelist.io) using the new API.

**Key improvments over the old version**
* Search with imdb_id if available
* Posibility to search in multiple categories
* No more scraping, API returns JSON data

**Known limitations**
* Currently API doesn't provide a way to sort result. [sort_by](https://flexget.com/Plugins/sort_by) plugin can be used for this, see example.
* Acording to API documentation, rate limit is set to 150 request per hour, during developent I have discovered that the rate limit is actually 150 requests per 15min, so there is no rate limit implemented, should we need one we will revisit the topic.

## Configuration
Requires username and passkey. Passkey can be retrieved from [profile](https://filelist.io/my.php).

```
filelist:
  username: xxxxxxx
  passkey: xxxxxx
  category: one or more #default all categories, see below complete list.
  internal: yes|no #default no, search only internal torrents .
  moderated: yes|no #default no, search only moderated torrents -- not exacly sure what this does.
  freeleech: yes|no #default no.
  doubleup: yes|no #default no.
```

**Categories**
```
Anime 
Audio 
Desene
Diverse
Docs
FLAC
Filme 3D
Filme 4K
Filme 4K Blu-Ray
Filme Blu-Ray
Filme DVD
Filme DVD-RO
Filme HD
Filme HD-RO
Filme SD
Jocuri Console
Jocuri PC
Linux
Mobile
Programe
Seriale 4K
Seriale HD
Seriale SD
Sport
TV
Videoclip
XXX
```
## Example Usage

```
tasks:
    movies-discover:
    template: movies
    sort_by:
      - field: torrent_seeds
        reverse: yes    
    discover:
      what:
        - movie_list: 
            list_name: movies
            strip_year: yes
      from:
        - filelist_api: 
            username: '{? filelist.username ?}'
            passkey: '{? filelist.passkeys ?}'
            category: ['Filme 4K', 'Filme 4K Blu-Ray']
            internal: yes
            freeleech: yes
      release_estimations:
        optimistic: 21 days
```