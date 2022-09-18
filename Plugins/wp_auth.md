---
title: wp_auth
description: 
published: true
date: 2022-09-18T05:16:53.274Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:16:50.676Z
---

# WordPress Authorization
Access WordPress [s2Member](https://s2member.com/) protected RSS feeds.
## Example
```
wordpress_auth:
      url: <wordpress login-page>
      username: <wordpress username>
      password: <wordpress password>
```
## Options
Only the `url` field is required.

| Name | Description |
| --- | --- |
| `url` | The WordPress login page for the membership site (usually `wp-login.php`) |
| `username` | WordPress username |
| `password` | WordPress password |
