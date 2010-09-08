To grab a series from NZBClub.com you can use their RSS feed, but it needs some urlrewrite and the filenames are absolutely terrible by default. Requires version r1333 or newer.[[BR]]
[[BR]]
Here is an example for the feed http://nzbclub.com/nzbfeed.aspx?ps=teevee&sa=1&sp=1 - it's a RSS feed for everything the user teevee posted (you can create your own feed for different subjects at nzbclub.com).[[BR]]
[[BR]]
{{{
presets:
  tv:
    series:
      720p:
        - series 1
        - series 2
    content_size:
      min: 150
      max: 1500
    download: /home/user/sabnzbd/nzbfiles/series/

feeds:
  nzbclub:
    preset: tv
    rss: 
      url: http://nzbclub.com/nzbfeed.aspx?ps=teevee&sa=1&sp=1
      filename: no                                               # prevent ugly names from the rss
    urlrewrite:
      nzbclub:
        regexp: http://nzbclub.com/nzb_view.aspx
        format: http://nzbclub.com/nzb_download.aspx
    manipulate:                                                  # remove all crap from the title
      - title:
          extract: .*\[\s*(.*)\s*\]-.*
    set:                                                         # prevent content-disposition being used, causing filename to fallback to (now clean) title
      content-disposition: no
}}}