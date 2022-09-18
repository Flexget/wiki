---
title: headers
description: 
published: true
date: 2022-09-18T05:06:10.016Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:06:07.407Z
---

# Headers
Allows editing request headers. This will affect most of the plugins in a task (everything that uses urllib2).

**Example: cookies**

Check out [cookies](/Plugins/cookies) plugin as well.

To use feeds that require login, setting cookie is usually required. You will need to extract the cookie for site and grab details from it (often uid, pass).

### Configuration
```
headers:
  Cookie: "uid=3945; pass=f8bae52ca325b14ef2523fabc"
```

### How to find cookie information
 * IE users will find their cookies in %UserProfile%\Cookies
 * Firefox users will find their cookies in Tools -> Options -> Privacy -> Cookies -> Show Cookies. (or the addon Export cookies may be used)
 * Opera users will find their cookies in Tools -> Advanced -> Cookies

## Security warning
Setting headers in a task will affect most of the HTTP request made in the task. This means that the values you set in the headers can be leaked to some unintended services as well.