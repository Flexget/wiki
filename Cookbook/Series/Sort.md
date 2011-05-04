= Sort downloads =

This recipe is to sort your already downloaded series into their own folders.

{{{
presets:

  # this preset cannot have any other configuration or else it will affect our sort-series
  tv-series:
    series:
      - Chuck
      - Eureka
      - Big Bang Theory
      - True Blood
      - Dollhouse
      - House
      - Persons Unknown
  
feeds:

  download-rss:
    rss: ...
    presets:
      - tv-series
    download: ...

  sort-series:
    find:
      path: /storage/downloads/
      regexp: '.*\.(avi|mkv)$'
    disable_builtins: [seen]
    preset: tv-series
    set:
      immortal: yes
      path: /storage/series/%(series_name)s/Season %(series_season)02d
    plugin_priority:
      set: 255
    if:
      - has_field('series_name'): accept
    exec: mkdir -p "%(path)s" && mv "%(location)s" "%(path)s/"
}}}
'''Uses Plugins:'''

 - [wiki:Plugins/find find]: In this recipe, we use find which creates an entry for each file in the specified path (/storage/downloads/ in this case,) that match the regexp pattern specified.
 - [wiki:Plugins/disable_builtins disable_builtins]: We disable the builtin seen plugin so that the series plugin will still parse titles that flexget has already seen (while downloading the first time.)
 - [wiki:Plugins/series series]: The series plugin is used to grab the series info (name, season, episode) from each file. We must list out all the series we want sorted.
 - [wiki:Plugins/set set]: We use the set plugin to build the new path for the files, using the variables added by the series plugin. We also set the immortal flag to prevent the series plugin from rejecting any entries.
 - [wiki:Plugins/plugin_priority plugin_priority]: The set plugin runs after the series plugin does it's filtering by default, so we have to change it's priority so that the immortal flag gets set before the series plugin does it's filtering.
 - if: We use the if plugin to accept any series that have the series_name field. (i.e. the entries that the series plugin successfully parsed)
 - [wiki:Plugins/exec exec]: We use the adv_exec plugin to create the path, then issue the move command. If there are other files in the directory, that the series plugin cannot parse, they will be skipped and remain in the original directory.


[wiki:Cookbook Back to The Cookbook]