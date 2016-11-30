# Couchpotato List
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; This is part of [managed list](/Plugins/List) plugin system.
</div>

Creates an [Entry](/Entry) for each movie in your [couchpotato](https://couchpota.to/) wanted list. This plugin can be used with the [movie_list ](/Plugins/List/movie_list) plugin to add those movies to the list.

## Plugin Settings
Currently the following settings are required:


|  Option  |  Description  |
| --- | --- |
| **base_url** | This is the URL of your couchpotato installation (usually http://localhost). If not specified otherwise, assumes the port is 80 by default.  |
| **api_key** | This is API key of your couchpotato installation (can be found under settings->general->advanced)   |
| **include_data** | Flag that enables whether to send Couchpotato's quality profile to FlexGet. Default is False   |

The following setting are optional:


|  Option  |  Description  |
| --- | --- |
| **port** | This is the port used by your couchpotato installation (usually 5050). Use this if your CP installation is at a different port than 80 (which it probably is).  |

### Example: add movies to the movie list
```
queue_movies_couchpotato:
    couchpotato_list:
      base_url: http://localhost
      port: 5050
      api_key: <your key here>
      include_data: yes
    accept_all: yes
    list_add:
      - movie_list: from couchpotato
```

For more information about list action go to the [list_interface](/list_interface) page.