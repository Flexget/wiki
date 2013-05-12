= Plex  =

Produces an entry for each show present in a  [http://www.plexapp.com Plex Media Server] TV section. Useful with [wiki:Plugins/import_series import_series] plugin.

== Configuration ==
Username and password for the website are the only configuration options:
Available configuration parameters:
||Name||Default||Mandatory||Description||
||server||localhost||No||Hostname/IP of PMS||
||port||32400||No||Port that PMS listens on||
||section||N/A||Yes||Section number to use as input, locate it at http://<yourplexserver>:32400/library/sections/||

== Sample configuration ==

{{{
import_series:
  from:
    plex:
      section: 3
      server: 192.168.1.23
      port: 32401
}}}
