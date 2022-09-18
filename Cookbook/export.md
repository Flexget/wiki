---
title: export
description: 
published: true
date: 2022-09-18T04:56:53.346Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:56:50.756Z
---

Because upgrade 1.x > 2.x broke some functions, I must reset all the config directory.

So i have backup my config directory.

#### The Series plugin
Go to the old directory to export the data...

```
sqlite3 db-config.sqlite

sqlite> .mode csv
sqlite> .out series.csv
sqlite> select max(season) , max(number), identifier, name from series_episodes as e join series as s where s.id = e.series_id group by e.series_id ;
sqlite> .exit

awk -F "," '{ print "flexget series begin "$4 " " $3 }' series.csv >> insert_series.sh
bash insert_series.sh
```

#### The Seen plugin
Go to the old directory to export the data...

```
sqlite3 db-config.sqlite

sqlite> .mode csv
sqlite> .out seen.csv
sqlite> select title from seen_entry ;
sqlite> .exit

awk -F "," '{ print "flexget seen add "$1 }' seen.csv >> insert_seen.sh
bash insert_seen.sh
```

kiss sor4.
