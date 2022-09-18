---
title: anirena
description: 
published: true
date: 2022-09-18T05:22:23.791Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:22:21.297Z
---

# Anirena
```
urlrewrite:
  aniarena:
    regexp: 'http://www.anirena.com/viewtracker.php\?action=details&id=(?P<id>\d+)'
    format: 'http://www.anirena.com/viewtracker.php?action=download&id=\g<id>'
```