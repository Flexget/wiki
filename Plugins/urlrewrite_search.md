---
title: urlrewrite_search
description: 
published: true
date: 2022-09-18T05:16:29.986Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:16:27.393Z
---

# Search

Use entry title and try to search it from supported sites. Accepts list of [search plugins](/Plugins/Searches) in order of priority. If entry is not found from any of the sites it will be rejected.

This can be used when there is no other way to get working download URL, ie. when input plugin does not provide any relevant URLs only titles. When relying on searching please make sure you're not querying too much, use [interval](/Plugins/interval) plugin to limit searches between few hours.

### Example

```yaml
urlrewrite_search:
  - newtorrents
  - piratebay: yes
  - nzbmatrix:
      apikey: myapikeyfromnzbmatrix
      username: myznbmatrixusername
      catid: 2
```
