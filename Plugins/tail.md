---
title: tail
description: 
published: true
date: 2022-09-18T05:14:07.567Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:13:55.881Z
---

# Tail
Similar to the [text](/Plugins/text) plugin but remembers the file position and continues from it. This plugins does NOT work for log files that are rotated.

**Example:**

```
tail:
  file: ~/irclogs/some/log
  entry:
    title: 'TITLE: (.*) URL:'
    url: 'URL: (.*)'
  encoding: utf8
```

The default encoding will be utf8 if none has been specified in the config. If you are getting `?` instead of non-ascii characters in your entries, you have likely specified the wrong encoding.

If the log file is detected to be smaller than in previous scan the position will be reset to the begining.

To reset file position manually use `execute --tail-reset <file>`