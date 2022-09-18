---
title: allyoulike
description: 
published: true
date: 2022-09-18T05:24:51.199Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:22:17.394Z
---

# allyoulike.com urlrewriter
    
Version 0.1

Rewrites urls for allyoulike.com

On allyoulike, each link points to a page which contains the links to the actual files. Often these pages contain links to more than one quality (for example 1080p, 720p etc.). The plugin chooses the set of links with the most files which should translate into the best quality movie.

If more than one valid link is found, the url of the entry is rewritten to the first link found. The complete list of valid links is placed in the 'urls' field of the entry.

Therefore, it is recommended, that you configure your output to use the 'urls' field instead of the 'url' field.

Below is an example configuration that uses the html plugin as input and the exec plugin as output. Note: the `~/.flexget/folderwatch folder is used by the folderwatch plugin of jDownloader to perform the actual download.

```yaml
  html:
    url: "http://www.allyoulike.com/category/movies/"
    title_from: link
    links_re:
      - allyoulike.com/\d*/(?!renew-or-purchase|for-vip-members-only)[^/]*/$
  exec:
    - echo "->{{movie_name}}<-" >> "~/.flexget/folderwatch/{{title}}.crawljob"
    - echo "text={{urls}}" >> "~/.flexget/folderwatch/{{title}}.crawljob"
    - echo "packageName={{title}}" >> "~/.flexget/folderwatch/{{title}}.crawljob"
    - echo autoConfirm=TRUE >> "~/.flexget/folderwatch/{{title}}.crawljob"
    - echo autoStart=TRUE >> "~/.flexget/folderwatch/{{title}}.crawljob"
```
In addition you will need to add a filtering plugin such as [list_match](/Plugins/List/list_match) or [series](/Plugins/series) to filter which content you actually want to download.
