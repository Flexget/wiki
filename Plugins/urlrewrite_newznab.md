= Newnzab plugin =

The newznab plugins is used in conjunction with the [wiki:Plugins/discover discover] plugins.

With the [wiki:Plugins/emit_series emit_series]
{{{
discover:
  what:
    - emit_series : yes
  from: 
    - newnab:
}}}

or the [wiki:Plugins/emit_movie_queue emit_movie_queue]

{{{
discover:
  what:
    - emit_movie_queue : yes
  from: 
    - newnab:
}}}


You need then to configure the newznab plugins, which take 4 parameters :
- website: website of the newznab server
- apikey:  mosst newznab requires this key in order to make search on their website
- category: type of search to do on newznab tv or movie
- wait  interval between two newznab call : (default  30 seconds)