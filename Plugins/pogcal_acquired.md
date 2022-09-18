---
title: pogcal_acquired
description: 
published: true
date: 2022-09-18T05:09:59.954Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:09:57.411Z
---

# Pogcal Acquired
This plugin marks the checkbox for accepted episodes on the [pogdesign TV calendar](http://pogdesign.co.uk/cat).

**Notes:**
- This will only work for episodes that aired during the same month you download them.
- The release numbering must match up with the numbering on pogdesign for it to work. (Date and sequence type shows will not work.)
- The show name normalization probably needs some improvement to match the names on the tv calendar. Feel free to [report an issue](https://flexget.com/newticket) for shows that are not working.

### Configuration
This plugin takes just two options, your username and password at the pogdesign calendar.
```
pogcal_acquired:
  username: me@internet.com
  password: itsasecret
```