= Email =

Send an e-mail with the list of all succeeded (downloaded) entries.

The result email will look like this:

{{{
Subject: [FlexGet] feedname : X new entries downloaded
Content: 
FlexGet has just downloaded X new entries for feed feedname  :
- release title (torrent url) => destination folder
- release title (torrent url) => destination folder
- release title (torrent url) => destination folder
- release title (torrent url) => destination folder
}}}

{{{
Config:
  from          : the email address from which the email will be sent (required)
  to            : the email address(es) of the recipient(s) (required)
  smtp_host     : the host of the smtp server
  smtp_port     : the port of the smtp server
  smtp_login    : should we use anonymous mode or login to the smtp server ?
  smtp_username : the username to use to connect to the smtp server
  smtp_password : the password to use to connect to the smtp server
  active        : is this module active or not ?
}}}

Config basic example:

{{{
email:
  from: xxx@xxx.xxx
  to: xxx@xxx.xxx
  smtp_host: smtp.host.com
}}}

Config example with smtp login and multiple recipients:

{{{
email:
  from: xxx@xxx.xxx
  to:
    - xxx@xxx.xxx
    - yyy@yyy.yyy
  smtp_host: smtp.host.com
  smtp_port: 25
  smtp_login: true
  smtp_username: my_smtp_login
  smtp_password: my_smtp_password
}}}

Config multi-feed example:

{{{
presets:
  global:
    email:
      from: xxx@xxx.xxx
      to: xxx@xxx.xxx
      smtp_host: smtp.host.com

feeds:
  feed1:
    rss: http://xxx
  feed2:
    rss: http://yyy
    email:
      active: False
  feed3:
    rss: http://zzz
    email:
      to: zzz@zzz.zzz
}}}

Default values for the config elements:

{{{
email:
  active: True
  smtp_host: localhost
  smtp_port: 25
  smtp_login: False
  smtp_username:
  smtp_password:
}}}

Gmail example:
{{{
    from: from@gmail.com
    to: to@gmail.com
    smtp_host: smtp.gmail.com
    smtp_port: 587
    smtp_login: true
    smtp_username: gmailUser
    smtp_password: gmailPassword
    smtp_tls: true
}}}