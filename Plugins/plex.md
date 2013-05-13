= Plex  =

Produces an entry for each show present in a  [http://www.plexapp.com Plex Media Server] TV section. Useful with [wiki:Plugins/import_series import_series] plugin.

== Configuration ==
Available configuration parameters:
||Name||Default||Mandatory||Description||
||server||localhost||No||Hostname/IP of PMS||
||port||32400||No||Port that PMS listens on||
||selection||all||No||Default selection to use, listing can be found at http://<yourplexserver>:32400/library/sections/<section>/||
||section||N/A||Yes||Section number to use as input, locate it at http://<yourplexserver>:32400/library/sections/||
||username||N/A||No||Myplex username, for logging in to remote servers||
||password||N/A||No||Myplex password, see above||

Using selection 'all' or 'recentlyViewedShows' will only produce a list of show names while the others will produce filename and download url.

== Sample configuration ==
Server on local network used as input for show listing:
{{{
import_series:
  from:
    plex:
      section: 3
      server: 192.168.1.23
      port: 32401
}}}

Remote server with Myplex authentication:
{{{
plex:
  section: 3
  server: my.remote.plex.server.com
  selection: recentlyAdded
  username: myplexusername
  password: myplexpassword
download:
  path: /mnt/downloads/
}}}
