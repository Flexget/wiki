= Reasoning 

Season packs can be a great source quickly download/back filling required episodes.
With a well-formed season pack this would actually be preferable for back-filling. This would also empower the search plugin.

= Problem

* Flexget currently handles each torrent file as a unique entity, and season packs do not conform to that schema.
* Passing on parts of the torrent file is a feature not guaranteed to be supported in all torrent clients (**Research needed**)
* At least one popular tracker has adopted removing all season episodes and reposting as season packs as soon as a season is complete.

= Proposed solution

If we could iterate over contents of season packs and treat each file as its own entity, or create separate torrent files just for missing files...