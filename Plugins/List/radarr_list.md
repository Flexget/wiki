# Radarr list
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; This is part of [managed list](/Plugins/List) plugin system.
</div>

Integrate with Radarr.

|  Option  |  Description  |
| --- | --- |
| **base_url** | Radarr location |
| **port** | Radarr port |
| **api_key** | Radarr API key |
| **only_monitored** | ? |
| **include_data** | ? |
| **only_use_cutoff_quality** | ? |


**Example:**

Use Radarr as input


```
radarr_as_input:
  radarr_list:
    base_url: "http://127.0.0.1"
    api_key: d2bcc5ec0c894b9587b6fbc3ff6ec11e
    port: 7878
    include_data: True
  accept_all: yes
```

**Example:**

Add entries from RSS feed into Radarr:

```
rss: "http://example.com"
accept_all: yes
list_add:
  - radarr_list:
      base_url: "http://127.0.0.1"
      api_key: d2bcc5ec0c894b9587b6fbc3ff6ec11e
      port: 7878
```

**Example:**

Use list_remove to remove items from Radarr:

```
remove_from_radarr_list:
  mock:
    - { title: "Ocean's Twelve (2004)", imdb_id: 'tt0349903', tmdb_id: 163 }
    - { title: 'Sinister 2 (2015)', imdb_id: 'tt2752772', tmdb_id: 283445 }
  accept_all: yes
  list_remove:
    - radarr_list:
        base_url: "http://127.0.0.1"
        api_key: d2bcc5ec0c894b9587b6fbc3ff6ec11e
        port: 7878
```

