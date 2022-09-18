---
title: domain_delay
description: 
published: true
date: 2022-09-18T05:04:03.864Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:04:01.246Z
---

# Domain Delay
Sets a minimum interval between requests to specific domains. Useful if you use a site that has a throttle on requests allowed.

**Example:**
```
domain_delay:
  mysite.com: 5 seconds
```