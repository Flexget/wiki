---
title: 
description: 
published: true
date: 2022-10-29T19:02:18.317Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:27:47.932Z
---

# Parse Only

If this option is set, the series plugin will not accept or reject any entries, it will merely fill in parsed metadata for the matching series on each entry. This can be useful if you want to reuse your series config on another task which may contain old episodes which you still want to act on.

If you use this option you will need some other filter plugin to accept the entries you want. If you wish to accept all entries parsed by the series plugin, you can use a combination of the [accept_all](/Plugins/accept_all) and the [require_field](/Plugins/require_field) plugin set to require the `series_name` field. 

Another popular option is to use [metainfo_series](/Plugins/metainfo_series) plugin based parsing that does not require series plugin with explicit series names. However it is not as accurate as series plugin with explicit names.
