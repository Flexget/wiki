== Set entry fields ==

Setting this key uses the [wiki:Plugins/set set] plugin to attach some information to each entry that matches the [#Perseriessettings series] or [#Groupsettings series group]. Other plugins may use this information to override their default settings for these entries. For example here is how it might be used to set the [wiki:Plugins/deluge deluge] {{{movedone}}} option for different series groups:

{{{
series:
  settings:
    720p:
      set:
        movedone: /media/TV/HD
    hdtv:
      set:
        movedone: /media/TV/SD
  720p:
    - Good Shows
  hdtv:
    - OK Shows
}}}
