= Send daily email of accepted downloads =

This will produce a daily email containing all downloads accepted from multiple different tasks. The email will be sent once per day no matter how often flexget is executed.

{{{
feeds:
  realfeeda:
    rss: http://something.com/feed.rss
    digest: daily email
    series:
      - good show

  realfeedb:
    rss: http://somethingelse.com/feed.rss
    digest: daily email
    series:
      - other show

  emailfeed:
    interval: 1 days
    emit_digest:
      list: daily email
    seen: local
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
