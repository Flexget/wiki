# From IMDB
This plugin creates [entries](/Entry) based on an IMDB person, company or character. Additional filters like content types and job types can be added to the config to limit down the generated list.
The main purpose of this plugin is to be used with the [movie_list](/Plugins/List/movie_list) plugin as an input, but it can be also used with [configure_series](/Plugins/configure_series) if content is set to TV.
This plugin is based on [IMDBPY](http://imdbpy.sourceforge.net/) and it is required ` pip install imdbpy `

## Plugin Settings
The only required setting is ID. The plugin can be used in several formats.
For example:
```
from_imdb: ch0001354
```
Or:
```
from_imdb: 
      id: ch0001354
```
More than one can be used:
```
from_imdb:
      id:
        - nm0004874 # Vin Diesel
        - nm0000246 # Bruce Willis
        - nm0000195 # Bill Murray 
        - nm0565250 # Melissa McCarthy
        - nm0005458 # Jason Statham
        - nm0000093 # Brad Pitt
        - nm0001125 # Benicio Del Toro
```
These two examples are equal. The only important part is to give the full IMDB ID in any form. Note that only person (`nm` prefix), company (`co` prefix) and character (`ch` prefix) are supported.


|  Option  |  Description  |
| --- | --- |
| **id** | As listed above, one or more strings that contains one of the prelisted accepted IMDB IDs. At least one is Required. **Note:** Each ID can potentially create a lot of requests and generate a lot of data. |
| **job_types** | A string or list with one or more of the following: `actor`, `director`, `producer`, `writer`, `self`, `editor`, `miscellaneous`, `editorial department`, `cinematographer`, `visual effects`, `thanks`, `music department`, `in development`, `archive footage` and `soundtrack`. Default is `actor`. Relevant only when filtering for `person`.  |
| **content_types** | A string or list with one or more of the following: `movie`, `tv series`, `tv mini series`, `video game`, `video movie`, `tv movie`, `episode`. Default is `movie` |
| **max_entries** |  The maximum number of entries that can return. This value's purpose is basically flood protection against unruly configurations that will return too many results. Default is `200`.  |
| **match_type** | Can be either `loose` or `strict`. Determines whether to check each item for its type before matching against content types. Default is `strict`. **__WARNING__** Switching to `loose` will dramatically improve performance but can result in undesired output. Best when used when `actor` or `actress` are **NOT** used. Recommended to run in test mode first to verify data. |



### Example:
```
tasks:
  auto-queue:
    from_imdb:
      id: nm0005212
      job_types:
        - actor
        - director
      content_types: tv series
    accept_all: yes
    list_add:
      movie_list: movies
```