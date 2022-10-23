---
title: plex
description: 
published: true
date: 2022-10-23T01:38:44.006Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:09:45.359Z
---

# Plex
**Note:** This plugin has been reported as incompatible with [PlexHome](https://blog.plex.tv/2014/11/20/introducing-plex-home/)*

Produces an entry for each show present in a  [Plex Media Server](http://www.plexapp.com) TV section. Can be used with [configure_series](/Plugins/configure_series) plugin or an output plugin.

## Configuration
Available configuration parameters:

| Name | Default | Mandatory | Description |
| --- | --- | --- | --- |
| server | localhost | No | IP or host of PMS |
| port | 32400 | No | Port that PMS listens on |
| selection | all | No | Default selection to use, listing can be found at http://\<yourplexserver>:32400/library/sections/\<section>/ |
| section | N/A | Yes | Section to use as input, numerical (/library/sections/\<num>) or section name. |
| username | N/A | No | Myplex username, for logging in to remote servers |
| password | N/A | No | Myplex password, see above |
| token    | N/A | No | [Plex Token](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/). Use it instead of username/password parameters but not both! |
| lowercase_title | No | No | Convert filename (title) to lower case. |
| strip_year | Yes | No | Remove year from title, ex: Show Name (2012) 01x01 => Show Name 01x01 |
| original_filename | No | No | Use filename stored in PMS instead of transformed name. lowercase_title and strip_year will be ignored. |
| unwatched_only | No | No | Only request unwatched media from PMS. |
| fetch | file | No | Run "flexget doc plex" for options. |
Using selection 'all' or 'recentlyViewedShows' will only produce a list of show names while the others will produce filename and download url.

    'selection'         Can be set to different keys:
        - all                   : Default
        - unwatched             :
        - recentlyAdded         :
        - recentlyViewed        :
        - recentlyViewedShows   : Series only.


## Sample configuration
Server on local network used as input for show listing:
```
configure_series:
  from:
    plex:
      section: 3
      server: 192.168.1.23
      port: 32401
```

Remote server with Myplex authentication:
```
plex:
  section: 3
  server: 111.222.333.444
  selection: recentlyAdded
  username: myplexusername
  password: myplexpassword
```

Remote Plex-Cloud Server:
```
plex:
  section: 1
  server: **.ric.plex.services  # You get Server URL from https://plex.tv/users/cpms
  port: 80
  selection: recentlyAdded
  token: ****** # only use token ore user/pw not both!
  username: myplexusername
  password: myplexpassword
```

