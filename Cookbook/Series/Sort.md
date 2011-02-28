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
      path: /storage/series/%(series_name)s/Season %(series_season)02d
    exec:
      on_output:
        for_rejected: mkdir -p "%(path)s" && mv "%(location)s" "%(path)s/"
        for_entries: mkdir -p "%(path)s" && mv "%(location)s" "%(path)s/"
}}}
'''Uses Plugins:'''

 - [wiki:Plugins/find find]: In this recipe, we use find which creates an entry for each file in the specified path (/storage/downloads/ in this case,) that match the regexp pattern specified.
 - [wiki:Plugins/disable_builtins disable_builtins]: We disable the builtin seen plugin so that the series plugin will still parse titles that flexget has already seen (while downloading the first time.)
 - [wiki:Plugins/series series]: The series plugin is used to grab the series info (name, season, episode) from each file. We must list out all the series we want sorted.
 - [wiki:Plugins/set set]: We use the set plugin to build the new path for the files, using the variables added by the series plugin.*
 - [wiki:Plugins/exec exec]: We use the adv_exec plugin to create the path, then issue the move command. We use for_entries as well as for_rejected to loop over all of the entries in the feed, as the series plugin will reject any episodes it has already seen while downloading them. If there are other files in the directory, that the series plugin cannot parse, they will be skipped and remain in the original directory.

^* Need r1376 or newer for the set plugin to process rejected entries^

[wiki:Cookbook Back to The Cookbook]