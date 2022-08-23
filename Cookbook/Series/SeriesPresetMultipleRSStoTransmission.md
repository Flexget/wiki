Execute commands below as Root with "sudo su -" command to install the Transmission and FlexGet packages.  (Debian, Ubuntu examples shown, for RedHat use "yum install" instead of "apt-get install".)

**Commands - (As Root)**
```
apt-get -y install transmission
apt-get -y install transmission-daemon
apt-get -y install python-pip
pip install flexget
pip install transmission-rpc
```


Edit the Transmission configuration file below to ensure that Transmission RPC settings are correct and will match values in the FlexGet config.yml file.  (PS: The rpc-password field will change from plain-text to hashed value when transmission-daemon is restarted or reloaded to one-way encrypt the password.  That's okay and how it is supposed to work, don't change it back after that.)

**/etc/transmission-daemon/settings.json**
```
"rpc-enabled": true,
    "rpc-username": "user",
    "rpc-password": "transmission",
    "rpc-authentication-required": true,
    "rpc-bind-address": "0.0.0.0",
    "rpc-port": 9091,
    "rpc-url": "/transmission/",
    "rpc-whitelist-enabled": true,
    "rpc-whitelist": "127.0.0.1,10.*.*.*",
```

Create a new FlexGet config.yml to specify your settings.  Change the download path from "/mnt/data/Series/{{series_name}}" to where ever you want to store your files, change list of series to download, and change list of RSS feeds to download from.  Feel free to downgrade or remove the quality setting from 720p to hdtv to capture standard-quality shows.  (It is highly recommend that you create the configuration file under the home path of a regular, non-root, user account for security reasons.)

Warning: If the "removewhendone" field is set to "yes" then any the torrents in Transmission client, even ones not from FlexGet, will be automatically deleted once they are completed or incomplete and paused or stopped.  Be careful with it because if FlexGet gets executed hourly by cron and you have any incomplete paused torrents they will be deleted also even if they are not from FlexGet.  It is better to leave this setting as "no" so you can figure out what was downloaded by FlexGet by using the Transmission web interface on port 9091 and the completed torrents there and removing them manually if you wish.  (The code in "plugin_transmission.py" is currently (2012-02-26) broken because of the check "if transfer.status == 'stopped' and transfer.uploadRatio >= transfer.seedRatioLimit:" which happens to delete incomplete torrents that you have been trying to download for a long time and you happened to seed more data than the upload ratio that is globally set in Transmission by default.  Happened to me.)

Note: If the Manipulate section is uncommented it will remove the leading "The" from all feed results in the metainfo phase before any of the other plugins start processing creating a preferred way of series since so many of them start with "The".  If this is uncommented this will also require all TV series names specified below to be modified remove the leading "The" in the name to match the manipulated results, so that if you uncomment this you would also change "The Office" to "Office" below to match the newly manipulated results.  (This is a personal preference and it is up to you.)

**~/.flexget/config.yml**
```
templates:
  tv:

#    manipulate:
#      - title: &the
#          replace:
#            regexp: '^The\W'
#            format: ''
#      - filename: *the
#      - series_name: *the

    private_torrents: no

    series:
      settings:
        tv:
          exact: yes
          propers: 3 days
          quality: 720p+
          set:
            path: /mnt/data/Series/{{series_name}}
      tv:
        - Archer
        - Beavis and Butt-head
        - Big Band Theory
        - Breaking Bad
        - Dexter
        - Fringe
        - Game of Thrones
        - Mad Men
        - MythBusters
        - The Office
        - Real Time with Bill Maher
        - South Park
        - True Blood

    transmission:
      enabled: yes
      host: localhost
      port: 9091
      username: user
      password: transmission
      removewhendone: no

tasks:
  bt-chat.com-tv:
    priority: 1
    rss: http://rss.bt-chat.com/?group=3
    template: tv

  ezrss.it:
    priority: 2
    rss: http://ezrss.it/feed/
    template: tv

  thepiratebay.org-tv:
    priority: 3
    rss: http://rss.thepiratebay.org/208
    template: tv
    verify_ssl_certificates: no

  kat.ph-tv:
    priority: 4
    rss: http://kat.ph/tv/?rss=1
    template: tv

  extratorrent.com-tv:
    priority: 5
    rss: http://extratorrent.com/rss.xml?cid=8
    template: tv

  torrentz.eu-tv:
    priority: 6
    rss: http://torrentz.eu/feed
    template: tv

  showrss.karmorra.info-tv:
    priority: 7
    rss: http://showrss.karmorra.info/feeds/all.rss
    template: tv
```

Use the command below to edit your crontab file for the user account where FlexGet will run so that it polls the RSS feeds hourly.

**Commands - (As User)**
```
crontab -e
```

Add line below to the user's crontab file.

```
@hourly /usr/local/bin/flexget execute --cron
```