= Search =

'''To be introduced in 1.0'''

Search for download URL from supported sites. Accepts list of search modules in order of priority.

Once hit has been found no more searches are performed. Should be used only when
there is no other way to get working download URL, ie. when input module does not provide
any downloadable URLs.

Example:

{{{
search:
  - newtorrents
  - piratebay
}}}

Notes:

 * Some resolvers will use search modules automatically if entry URL points into a search page.