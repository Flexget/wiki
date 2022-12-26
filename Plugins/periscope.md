---
title: periscope
description: 
published: true
date: 2022-12-05T03:36:39.816Z
tags: dependencies, abandoned
editor: markdown
dateCreated: 2022-09-18T05:09:41.587Z
---

# Periscope

>Project abandoned? Last release was 2011
{.is-danger}

>This plugin requires the `periscope` library. 
{.is-warning}

To install it, run:
```cmd
pip install periscope
```

Download subtitles for entries referred to existing video files.

## Options

| **Name** | **Info** | **Description** |
| --- | --- | --- |
| languages | Array | List of preferred languages: must be a ISO 639-1 code (2 digits) |
| alternatives | Array | List of secondary languages: subtitles in this list are downloaded, but the entry will be processed again until one for the `languages` list is found |
| subexts | Array | List of subtitles file extensions to check (for `overwrite` exclusive use) |
| overwrite | [yes|no](/yes|no) | Ignore videos already subbed (check for file with the extensions defined in the `subexts` list) |

**Example (complete task):**

```yaml
subtitles:
    filesystem:
      path: 
        - d:\media\incoming
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
    accept_all: yes
    periscope:
      languages:
        - it
      alternatives:
        - en
        - fr
      overwrite: yes
```
