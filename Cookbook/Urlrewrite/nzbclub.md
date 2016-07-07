To grab a series from NZBClub.com you can use their RSS feed, but it needs some urlrewrite and the filenames are absolutely terrible by default. Requires version r1333 or newer.  
  
Here is an example for the feed http://nzbclub.com/nzbfeed.aspx?ps=teevee&sa=1&sp=1 - it's a RSS feed for everything the user teevee posted (you can create your own feed for different subjects at nzbclub.com).  
  
```
templates:
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
    template: tv

    rss: 
      url: http://nzbclub.com/nzbfeed.aspx?ps=teevee&sa=1&sp=1
      # prevent ugly names from the rss
      filename: no

    # proper download links via urlrewrite
    urlrewrite:
      nzbclub:
        regexp: http://(www.)?nzbclub.com/nzb_view
        format: http://nzbclub.com/nzb_download

    # remove all crap from the title
    manipulate:                                                  
      - title:
          extract: \[\s(.*)\s\](/\s(.*)\s\)

    # prevent content-disposition being used, causing filename to fallback to (now clean) title
    set:
      content-disposition: no
```