= TVTorrents =

A customized HTML input module. Parses out full torrent URLs from [http://tvtorrents.com TVTorrents]' page for recently aired TV show episodes.

May break in the future, as it depends on the exact structure of the HTML.

Plugin-specific code by Fredrik Bränström.

== Usage ==

Just set '''tvt: yes''' and configure [wiki:Plugins/cookies cookies] plugin.

== Example ==

{{{
feeds:
  TVTorrents:
    tvt: yes
}}}
