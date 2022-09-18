---
title: verify_ssl_certificates
description: 
published: true
date: 2022-09-18T05:16:41.618Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:16:39.086Z
---

# Verify SSL Certificates

Can turn off SSL certificate verification on a task. Useful if you have e.g. an https [rss](/Plugins/rss) input which does not have a valid certificate.
```
verify_ssl_certificates: no
```

**`WARNING:`** Make sure you understand the risks before disabling SSL certificate verification on a task. This plugin will affect every HTTPS network request in that task.