To grab series from NZBClub.com you can use their RSS feed, but it needs some urlrewrite.[[BR]]
[[BR]]
Here an example for the feed http://nzbclub.com/nzbfeed.aspx?ps=teevee&sa=1&sp=1 - it's a RSS feed for everything the user teevee posted (you can create your own feed for different subjects at nzbclub.com)[[BR]]
[[BR]]
{{{
presets:
  series:
    720p:
      - series 1
      - series 2

feeds:
  nzbclub:
    rss: http://nzbclub.com/nzbfeed.aspx?ps=teevee&sa=1&sp=1
    download: /home/user/sabnzbd/nzbfiles/series/
    preset: series
    content_size:
      min: 150
      max: 3000
    urlrewrite:
      nzbclub:
        regexp: http://nzbclub.com/nzb_view.aspx
        format: http://nzbclub.com/nzb_download.aspx
    manipulate:
      title:
        from: title
        regexp: .*\[\s*(.*)\s*\]-.*
    interval: 10 minutes
}}}

If you even want to keep nicer job names you can add something like this:

{{{
    exec: "mv %(output)s /real/watch/dir/path/%(title)s.nzb"
}}}

