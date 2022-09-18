---
title: rlsbb
description: 
published: true
date: 2022-09-18T05:11:12.606Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:11:09.957Z
---

# Url Rewriter for rlsbb.ru
Read [how URL rewriting works](/URLRewriters).

The feed from rlsbb.ru contains only a few links of varying quality in its content field (which is only accessible in flexget since version 2.10.67). This plugin allows to filter those links for certain filehosters and qualities. It is also possible to search the comments of posts for additional links (for example to other filehosters of better quality).

If more than one valid link is found, the plugin puts them as an array into the `urls` field of the entry.

## Configuration

### filehosters_re

You can filter links to which filehosters should be grabbed by adding regular expressions to the `filehosters_re` configuration parameter. You can also filter for certain qualities in this configuration paramter.

**Example:**

```yaml
  rlsbb:
    filehosters_re:
      - domain\.com.*(720p|1080p)
      - domain2\.org.*1080p
```

Assuming there are the following links on the rlsbb.ru download page:

```html
http://domainx.cr/CoolFile.avi
http://domain.com/CoolFile.720p.avi
http://domain2.org/CoolFile.1080p.part1.avi
http://domain2.org/CoolFile.1080p.part2.avi
```
The plugin would rewrite the `url` field of the entry to:
```html
http://domain2.org/CoolFile.720p.avi
```
and would add the `urls` field containing an array of links:
```html
['http://domain.com/CoolFile.720p.avi',
'http://domain2.org/CoolFile.1080p.part1.avi',
'http://domain2.org/CoolFile.1080p.part2.avi']
```
### parse_comments

If you want to also parse the comments of the respective post on rlsbb.ru, add `parse_comments: yes` to the configuration. The filters configured in `filehosters_re` will also be applied to the links found in the comments.

**Example:**
```yaml
  rlsbb:
    parse_comments: yes
    filehosters_re:
      - domain\.com.*(720p|1080p)
      - domain2\.org.*1080p
```

### link_text_re

This is an advanced configuration option, which is useful in case rlsbb.ru changes the layout of their page. On the rlsbb.ru page, the links are marked with the text `UPLOADGiG`, `NiTROFLARE` or `RAPiDGATOR`. The plugin looks for this text and grabs links it finds there. In case rlsbb.ru changes/adds these texts, you can change the default configuration:
```yaml
  rlsbb:
    link_text_re:
      - UPLOADGiG
      - NiTROFLARE
      - RAPiDGATOR
```


## Note:
Particularly in case the files are split into multiple parts, it is recommended that you configure your output to use the `urls` field of the entry.

***Example for JDownloader 2 (using the folderwatch extension):***
```yaml
  exec:
    - echo "text={{urls}}" >> "/path/to/jd2/folderwatch/{{title}}.crawljob"
```