---
title: sequence
description: 
published: true
date: 2022-10-14T16:57:05.575Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:12:34.200Z
---

# Sequence

Mainly for advanced usecases. Run any plugins in order. 

### Example:

Note: Using [inputs](/Plugins/inputs) plugin would be more appropriate use for this usecase.

```yaml
sequence:
  - rss: http://example1.com
  - rss: http://example2.com
```
