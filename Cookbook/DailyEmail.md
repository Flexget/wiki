= Send daily email of accepted downloads =

This will produce an email containing all downloads accepted from feeds that contain the rssout preset. The email will be sent once per day no matter how often flexget is executed.

{{{
rssout:
  make_rss: ~/downloaded.rss
    days: 1
feeds:
  realfeeda:
    rss: http://something.com/feed.rss
    preset: rssout
    series:
      - good show
  realfeedb:
    rss: http://somethingelse.com/feed.rss
    preset: rssout
    series:
      - other show
  emailfeed:
    interval: 1 day
    rss: file://~/downloaded.rss
    disable_builtins: [seen]
    accept_all: yes
    email:
      from: xxx@xxx.xxx
      to: xxx@xxx.xxx
      smtp_host: smtp.host.com
      smtp_port: 25
      smtp_login: true
      smtp_username: my_smtp_login
      smtp_password: my_smtp_password
}}}
