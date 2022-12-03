---
title: cfscraper
description: 
published: true
date: 2022-12-03T03:52:13.152Z
tags: dependencies
editor: markdown
dateCreated: 2022-09-18T05:02:41.285Z
---

# Cloudflare Scraper

<div class="alert alert-info" role="alert">
  <span class="glyphicon glyphicon glyphicon-download-alt"></span>
  &nbsp;
This plugin requires the cloudscraper Python library. To install it, run the following command:
<br/><br/>

```cmd
pip install cloudscraper
```

  <span class="glyphicon glyphicon glyphicon glyphicon glyphicon-info-sign"></span>
  &nbsp;
When Cloudflare updates its anti-bot measures, this plugin may cease to function. Upgraded version (if available) can be installed with:
<br/><br/>

```cmd
pip install --upgrade cloudscraper
```
</div>

Enables cloudflare scraping in a task. Useful if you are using [html](/Plugins/html) to scrape a site that utilizes Cloudflares anti-bot services.

```yaml
cfscraper: yes
```

