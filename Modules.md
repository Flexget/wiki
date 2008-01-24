= Modules =

Modules are !FlexGet essence. They provide all functionality by creating, manipulating or downloading [wiki:Entry entries]. !FlexGet has internal manual for all modules. Run program with {{{--list}}} to list all available modules. You can display manual and examples by using parameter {{{--doc <module>}}} (similar to this wiki).

=== Inputs ===

Produce [wiki:Entry entries] from external source.

[wiki:InputRSS RSS], [wiki:InputHtml Html], [wiki:InputCSV CSV], [wiki:InputRlsLog RlsLog]

=== Filters ===

Filter and accept feeds [wiki:Entry entries] based on configuration.

[wiki:FilterImdb Imdb], [wiki:FilterPatterns Patterns], [wiki:FilterSeries Series], [wiki:FilterUnconditionally Unconditionally], [wiki:FilterIgnore Ignore], [wiki:FilterSeen Seen]

=== Outputs ===

[wiki:OutputDownload Download]

=== Modify / Other ===

[wiki:ModifyRemoveTrackers Remove Trackers]

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
      - \[vegapunk\].*one.piece.*\d\d\d.HD  
    download: ~/torrents
}}}

Here we have a simple configuration file with two feeds called {{{tvrss combined}}}
and {{{vegapunk}}}. Both have single input module [wiki:InputRSS RSS] that expects url as a parameter.
This converts RSS into [wiki:entry entries] for our feed. 

Next we have filter module [wiki:FilterPatterns patterns]
that expects list of regular expressions. If [wiki:entry] does not match any of the regexps it will be filtered.

Last we have download module that simply downloads all remaining [wiki:Entry entries] and saves them to given path.

== Builtin modules ==

Some modules are enabled by default even when they are not mentioned in configuration file. This is because they're
needed in almost all situations ([wiki:FilterSeen seen]) or they make sure specific content is formatted 
properly and do not intervene in other cases ([wiki:ModifyTorrent torrent]).

=== How to disable builtins ===

{{{
disable_builtins: True
}}}