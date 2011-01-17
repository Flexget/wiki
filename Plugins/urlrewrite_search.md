= Search =

Use entry title and try to search it from supported sites. Accepts list of search plugins in order of priority. If entry is not found from any of the sites it will be rejected.

This should be used only when there is no other way to get working download URL, ie. when input plugin does not provide any relevant URLs.

== Example ==

{{{
search:
  - newtorrents
  - piratebay
  - nzbmatrix:
      apikey: myapikeyfromnzbmatrix
      username: myznbmatrixusername
      catid: 2
}}}

To get list of supported sites run flexget with `--search-plugins`

For the nzbmatrix search plugin, it requires apikey and username. All other arguments from http://nzbmatrix.com/api-info.php search API can also be set, with the exception of the "search" parameter.