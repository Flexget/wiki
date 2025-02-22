---
title: cfscraper
description: 
published: true
date: 2025-02-22T21:33:24.134Z
tags: dependencies
editor: markdown
dateCreated: 2022-09-18T05:02:41.285Z
---

# Cloudflare Scraper

> This plugin has been removed from [Flexget 3.15](https://flexget.com/UpgradeActions#h-3150-2025-02-08) onwards
{.is-warning}


This plugin requires the cloudscraper Python library. To install it, run the following command:

```cmd
pip install cloudscraper
```

When Cloudflare updates its anti-bot measures, this plugin may cease to function. Upgraded version (if available) can be installed with:

```cmd
pip install --upgrade cloudscraper
```

## Usage

Enables cloudflare scraping in a task. Useful if you are using [html](/Plugins/html) to scrape a site that utilizes Cloudflares anti-bot services.

```yaml
cfscraper: yes
```
