= Modules =

Modules are !FlexGet essence. They provide all functionality by creating, manipulating or downloading [wiki:Entry entries]. !FlexGet has internal manual for all modules. Run program with {{{--list}}} to list all available modules. You can display manual and examples by using parameter {{{--doc <module>}}} (similar to this wiki).

== Notes ==

All module documentation examples are on module level, meaning that they need to be under a feed in configuration. They are not sufficient alone. Look at [wiki:Configuration configuration] or complete examples if you have any open questions.

If you plan to use multiple filters per feed, you should look [wiki:FilterOperations filter operations] to understand what effect each module has in chain.

=== Inputs ===

Produce [wiki:Entry entries] from external source.

[wiki:InputRSS rss], [wiki:InputHtml html], [wiki:InputCSV csv], [wiki:InputRlsLog rlslog]

=== Filters ===

Filter, Reject or Accept feeds [wiki:Entry entries] based on given rules. Single feed may have any number of filters chained.

[wiki:FilterImdb imdb], [wiki:FilterPatterns patterns], [wiki:FilterSeries series], [wiki:FilterUnconditionally unconditionally], [wiki:FilterIgnore ignore], [wiki:FilterLimitNew limit_new], [wiki:FilterSeen seen]

=== Outputs ===

[wiki:OutputDownload download], [wiki:ModuleCookies cookies]

=== Modify / Other ===

[wiki:ModifyRemoveTrackers remove_trackers], [wiki:ModuleCliConfig cli_config]

=== TODO ===

[wiki:FilterExists exists], [wiki:FilterPatternsV2 patterns v2]

== So how does it all work? ==

Let's look real world configuration file.

{{{
feeds:
  tvrss combined:
    rss: http://tvrss.net/feed/unique/
    patterns:
      - south.park
    download: ~/torrents

  vegapunk:
    rss: http://bt.vegapunk.com/rss/rss.xml
    patterns:
      - ^\[vegapunk\].*one.piece.*\d\d\d.HD  
    download: ~/torrents
}}}

Here we have a simple configuration file with two feeds called {{{tvrss combined}}}
and {{{vegapunk}}}. Both have single input module [wiki:InputRSS RSS] that expects url as a parameter.
This converts RSS into [wiki:entry entries] for our feed. 

Next we have filter module [wiki:FilterPatterns patterns]
that expects list of regular expressions. If [wiki:entry] does not match any of the regexps it will be filtered otherwise it will be accepted.

Last we have download module that simply downloads all remaining [wiki:Entry entries] and saves them to given path.

== Builtin modules ==

Some modules are enabled by default even when they are not mentioned in configuration file. This is because they're
needed in almost all situations ([wiki:FilterSeen seen]) or they make sure specific content is formatted 
properly and do not intervene in other cases ([wiki:ModifyTorrent torrent]).

=== How to disable builtins ===

{{{
disable_builtins: true
}}}