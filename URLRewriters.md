# URL Rewriters
## What are they for

Many RSS-feeds (and other inputs) don't provide URLs directly to a torrent-file, but instead point to a download page, often with a completely different domain name. This makes these feeds almost useless for automating downloading in most of the applications. FlexGet overcomes this by providing clean and easy way to add custom functionality for such sites.

## How they work

Foremost: automatically and in the background!

URL Rewriters are special type of plugins that detect if any of the [entries](/Entry) in a feed point to a download page instead of actual content. When such a [entry](/Entry) is detected, the rewriter will step in and modify the URL so that it points into the actual desired content. This is usually achieved by editing URL or by requesting the download page and finding the correct download link from there.

URL Rewriters do not need to be configured aside from generic [urlrewrite](/Plugins/urlrewrite). URL rewriting happens automatically in the background for all supported sites.

### Supported

As of 2017-06 following rewriters are included. To get up to date list run command `flexget plugin --interface urlrewriter`.

* 1337x
* animeindex
* anirena
* archetorrent   
* bakabt         
* cinemageddon   
* deadfrog       
* divxatope      
* extratorrent   
* eztv           
* frenchtorrentdb
* google
* google_cse
* hliang
* iptorrents     
* koreus         
* newpct         
* newtorrents    
* nnm-club       
* nyaa           
* piratebay      
* [rmz](Plugins/rmz)
* serienjunkies  
* shortened      
* torrent411
* torrentday
* torrentleech   

### Custom rewriting with regexp

For unsupported sites you can often rewrite by using regexp. 

This works only when URL is only slightly different from the download page, see [urlrewrite](/Plugins/urlrewrite) plugin for more information.

## Not on the list? Make your own

Use existing rewriter as a starting point, it should be quite easy if you have any programming experience. DeadFrog rewriter is a good one to make a copy of and start hacking with it. If you make something, please [contribute it](/Contribute).