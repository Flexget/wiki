= Rtorrent connector =

Opens a Rtorrent XMLRPC connection and allows you to feed the session into FlexGet, or (''not yet implemented'') load output items directly into the client, including the transfer of metadata available in FlexGet.

If you use this plugin, you '''MUST''' `easy_install pyrocore` as an additional dependency. Follow the [http://code.google.com/p/pyroscope/wiki/QuickStartGuide installation guide] and [http://code.google.com/p/pyroscope/wiki/UserConfiguration configuration instructions] of PyroScope before adding the plugin configuration to FlexGet. Also see the [http://code.google.com/p/pyroscope/wiki/FlexGetPlugins PyroScope FlexGet Plugins] page.

'''''NOTE:''' This is a new plugin that has not yet matured, which doesn't imply that the code is not quite stable, but the feature-set is lacking so far, and in flux.''


== Configuration ==

The following settings control some basic behaviour:
 enabled:: Enable the plugin?

These keys are used to control reading the session memory of Rtorrent, i.e. using it as a feed:
 view:: The Rtorrent view that is used as a source of the feed items (default is `main`).
 feed_query:: A pyrocore [http://code.google.com/p/pyroscope/wiki/RtControlExamples#Fundamentals filter expression] that selects the items to pass on to FlexGet.



== Examples ==

=== Dump HDTV downloads of the last 2 days ===
Dump torrents matching a filter condition, note that both PyroScope (`feed_query`) and FlexGet (`quality`) filtering is used:
{{{
tasks:
  pyrotest:
    rtorrent:
      feed_query: 'loaded=-2d'
    quality: hdtv
    dump: yes

}}}

=== Change the location of config files ===
Overriding the normal PyroScope and Rtorrent configuration locations:
{{{
presets:
  global:
    rtorrent:
      config_dir: ~/.pyroscope_flex
      overrides:
        rtorrent_rc: ~/bittorrent/rtorrent.rc
}}}
Note that you '''MUST''' do this in the `global` preset, because right now, only a connection to ''one'' Rtorrent instance per FlexGet configuration is supported.


== Roadmap ==

 * Load torrent directly into rtorrent.
 * Set custom fields based on FlexGet data.
 * Use the Rtorrent session similarly to the exists_* and seen plugins.


== Ideas ==

 * Carry out some kind of nuke action when a proper or repack etc. arrives for a loaded torrent.
