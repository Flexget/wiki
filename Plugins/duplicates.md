---
title: duplicates
description: 
published: true
date: 2022-09-18T05:04:15.328Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:04:12.787Z
---

# Duplicates

Take action on entries with duplicate field values.

**Syntax:**

```code
duplicates:
  field: <field name>
  action: [accept|reject]
```

**Example:**

Move duplicate movies for manual review.

```yaml
tasks:
  duplicate-movies:
    manual: yes
    seen: no
    filesystem: /storage/movies
    imdb_lookup: yes
    duplicates:
      field: imdb_id
      action: accept
    move:
      to: /storage/movies-duplicates
      allow_dir: yes
```
