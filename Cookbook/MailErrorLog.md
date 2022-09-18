---
title: MailErrorLog
description: 
published: true
date: 2022-09-18T04:55:43.941Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:55:41.377Z
---

This is a simple script that sends all ERRORS, WARNINGS and CRITICALS in FlexGet's log file as an email.

Prerequisites:
 - logtail for following the flexget logfile
 - bsd-mailx for the -E option to not send mail if there is no content, GNU mailutils doesn't have a comparable option

Save the following as ~/bin/flexget_logwatch:
```/bin/sh
/usr/sbin/logtail -f$HOME/flexget/flexget.log |
grep -v INFO |
grep -v VERBOSE |
mail -E -s "Flexget logwatch" example@example.com
```

Remember to change the example address to your own =) You can use the -t option on logtail to test the script, it won't advance the read pointer in that case.

Then insert the script in your crontab:

```
@hourly ~/bin/flexget_logwatch
```

Now you will get an email every hour if there are new errors in FlexGet's logfile.