= Emit cleanup =

=== Problem description ===

We currently have multiple plugins with various different naming and configuration convention. These should be unified.

'''Group A'''

* trakt_emit
* sonarr_emit
* uoccin_emit 

'''Group B'''

* emit_digest
* emit_series

'''Group C'''

* from_deluge
* from_rtorrent
* from_transmission

'''Group D'''

special one [wiki:Plugins/subtitle_queue subtitle_queue] which can be configured to manage the queue OR emit the content with:

* subtitle_queue: emit

=== Thoughts ===

* emit is a bit weird term and "from_deluge" etc seem to make more sense than "emit_deluge"
* approach in subtitle_queue is kind of nice as then there is no need to have multiple registered plugins for one thing, although then you can not combine deluge input and deluge output in a same task for example
* best approach to rename everything to "from_<thing>" and create new "from_subtitle_queue" plugin to follow the convention?
* some of these should be converted into a list plugins? 