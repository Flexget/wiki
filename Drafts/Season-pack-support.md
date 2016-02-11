=Reasoning=

Season packs can be a great source quickly download/back filling required episodes. 

=Problem= 

* Flexget currently handles each torrent file as a unique entity, and season packs do not conform to that schema.
* Passing on parts of the torrent file is a feature not guaranteed to be supported in all torrent clients (**Research needed**)

=Proposed solution=

If we could iterate over contents of season packs and treat each file as its own entity, or create seperate torrent files just for missing files...