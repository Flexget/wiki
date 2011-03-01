= IMDB Queue Input =

Pulls out IMDB Queue and passes it to another plugin (intended to be used with the [wiki:Plugins/search search] plugin).

=== Example ===

{{{
emit_imdb_queue: yes
imdb_queue: yes
search:
  - nzbmatrix:
      apikey: nzbmatrixapikey
      username: nzbmatrixusername
      catid: 2
}}}

You should almost certainly use imdb_queue: yes with this, like below. As above, you should use the search plugin, or another plugin that adds a URL given a title, as this input does not have a url associated with each entry (like a normal input plugin).

{{{
imdb_queue: yes
}}}

=== Notes ===

 * Somewhat poorly tested
 * Emits names in IMDB translated form, making this pretty useless with [wiki:Plugins/search search] if you live somewhere where english isn't primary language.