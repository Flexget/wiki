= Search =

'''Note:''' To be introduced in 1.0

Search entry from sites. Accepts list of known search modules, list is in priority order.
Once hit has been found no more searches are performed. Should be used only when
there is no other way to get working download url, ie. when input module does not provide
any downloadable urls.

Example:

{{{
search:
  - newtorrents
  - piratebay
}}}

Notes:
 * Some resolvers will use search modules automaticly if enry url points into a search page.