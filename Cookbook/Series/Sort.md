= Sort downloads =

This recipe is to sort your already downloaded series into their own folders. Note that !FlexGet is not really made for sorting so this is a bit complicated and hackish.

{{{
presets:

  # NOTE!! This preset cannot have any other configuration or else it will affect our sort-series.
  # Also, you must use series groups, so that we can turn off filtering with the parse_only option in our sort feed.
  tv-series:
    series:
      agroup:
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
    # NOTE: You must set the parse_only option for all of the series groups you have configured in your preset.
    # This option prevents the series plugin from accepting or rejecting anything in this feed.
    series:
      settings:
        agroup:
          parse_only: yes
    # With the require_field and accept_all plugins, we accept anything that the series plugin has successfully parsed.
    require_field: series_name
    accept_all: yes
    move:
      to: /storage/series/{{series_name}}/Season {{series_season|pad(2)}}
}}}
'''Uses Plugins:'''

 - [wiki:Plugins/find find]: In this recipe, we use find which creates an entry for each file in the specified path (/storage/downloads/ in this case,) that match the regexp pattern specified.
 - [wiki:Plugins/disable_builtins disable_builtins]: We disable the builtin seen plugin so that the series plugin will still parse titles that flexget has already seen (while downloading the first time.)
 - [wiki:Plugins/series series]: The series plugin is used to grab the series info (name, season, episode) from each file. We must list out all the series we want sorted.
 - [wiki:Plugins/set set]: We set the immortal flag to prevent the series plugin from rejecting any entries. This is a bit hacky, and there should be a better way in the future.
 - [wiki:Plugins/move move]: We use the move plugin to move the file to a dynamic path based on the parsed series name and season. If there are other files in the input directory that the series plugin cannot parse, they will be skipped and remain in the original directory.


[wiki:Cookbook Back to The Cookbook]