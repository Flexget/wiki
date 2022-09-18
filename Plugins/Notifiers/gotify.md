---
title: gotify
description: 
published: true
date: 2022-09-18T05:25:45.140Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:25:42.529Z
---

# [Notifiers](/Plugins/Notifiers) > Gotify
> Gotify is a part of the [notifier](/Plugins/Notifiers) plugin system.
{.is-success}

This plugin provides the ability to send flexget notifications via the self-hosted Gotify notification server (https://gotify.net).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|**url**|URL|Gotify server URL **Required**|
| **token**| text| User's Gotify token. **Required**|
|priority|integer|Message priority. The Android client classifies messages by High (>7), Normal (4-7), Low (1-3) and Minimum priority (<1).|4
| content_type | text | Set content type. Can be `text/plain` or `text/markdown` | `text/plain`

### Examples

### Send notification for each accepted entry
```yaml
    notify:
      entries:
        via:
          - gotify:
              url: <GOTIFY_SERVER_URL>
              token: <GOTIFY_TOKEN>
              priority: <PRIORITY>
              content_type: "text/markdown"
```


