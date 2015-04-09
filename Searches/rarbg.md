= RarBG =
This search plugin will get results from [http://rarbg.com]

== Configuration ==
You can search in a single category:
{{{
rarbg: 
  category: x264 1080p
}}}

or in multiple categories:
{{{
rarbg: 
  category:
    - x264 720p
    - x264 1080p
}}}

== List of possible categories ==

* {{{x264 720p}}}
* {{{x264 1080p}}}
* {{{XviD}}}
* {{{Full BD}}}
* {{{HDTV}}}
* {{{SDTV}}}

'''Advanced:''' You can also use categories ID directly, you can find them on RarBG if you hover over category link. (eg. rarbg.com/torrents.php?'''category[]=45'''). Multiple categories are separated by semi-colons in the url.
{{{
rarbg: 
  category: 2
}}}
Or multiple category IDs:
{{{
rarbg: 
  category: [2, 5, 8, 9, 20, 15, 16]
}}}

== Other settings ==
* {{{sorted_by}}}: {{{seeders}}}, {{{leechers}}} or {{{last}}}. Defaults to {{{last}}} ie. sorted by newest.
* {{{limit}}}: number of torrents, supports 25, 50 or 100.
* {{{ranked}}}: {{{True}}} or {{{False}}}. Defaults to {{{True}}}, which means it will only show RarBG related torrents ie. yify releases are ignored.