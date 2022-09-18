---
title: mysql_input
description: 
published: true
date: 2022-09-18T05:11:36.896Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:56:54.532Z
---

You can use the [Exec](/Plugins/exec) plugin to pass certain fields of an entry to a MySQL database. Make yourself comfortable with basic MySQL syntax first [here](http://dev.mysql.com/doc/refman/5.6/en/index.html).

The correct command for [Exec](/Plugins/exec) on Win7 is as follows:
```
exec: <%SystemRoot%>\system32\cmd.exe /c <\PATH\TO\>mysql.exe -u <user> -p<pwd> --execute="INSERT INTO <table> VALUES ('{{<entry1>}}','{{<entry2>}}')" <database>
```
* Strings between brackets '<' and '>' represent values you need to fill in yourself: <%SystemRoot>; <\PATH\TO\>; <user>; <pwd>; <table>; <entry>; <database>
* Avoid space between your -p-trigger and your passphrase: -ppassword is correct, -p password isn't.
* You can of course extend the list of fields inserted in the database; always regard the `other_fields` option of the [rss](/Plugins/rss) plugin.

Please note the extended possibilities this basic tutorial in combination with other plugins.