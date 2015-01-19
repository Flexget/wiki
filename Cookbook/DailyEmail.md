= Send daily email of accepted downloads =

This will produce an email containing all downloads accepted from feeds that contain the rssout template. The email will be sent once per day no matter how often flexget is executed.

'''Notes:'''

 * Use this only if you absolutely want to limit emails once per day. For immediate email notification the [wiki:Plugins/email email] plugin alone is sufficient.
 * This has not been fully tested yet, might need some tweaks
 * A bit hackish and prevents you from using `make_rss` for other purposes
 * This can't be added in global template!

{{{
templates:
  rssout:
    make_rss:
      file: ~/downloaded.rss
      days: 1

feeds:
  realfeeda:
    rss: http://something.com/feed.rss
    template: rssout
    series:
      - good show

  realfeedb:
    rss: http://somethingelse.com/feed.rss
    template: rssout
    series:
      - other show

  emailfeed:
    interval: 1 days
    rss:
      url: file:///home/user/downloaded.rss
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
