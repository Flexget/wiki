Execute commands below as Root with "sudo su -" command to install the Transmission and FlexGet packages.  (Debian, Ubuntu examples shown, for RedHat use "yum install" instead of "apt-get install".)

'''Commands - (As Root)'''
{{{
apt-get -y install transmission
apt-get -y install transmission-daemon
apt-get -y install python-pip
pip install flexget
pip install transmissionrpc
}}}


Edit the Transmission configuration file below to ensure that Transmission RPC settings are correct and will match values in the FlexGet config.yml file.  (PS: The rpc-password field will change from plain-text to hashed value when transmission-daemon is restarted or reloaded to one-way encrypt the password.  That's okay and how it is supposed to work, don't change it back after that.)

'''/etc/transmission-daemon/settings.json'''
{{{
    "rpc-enabled": true,
    "rpc-username": "user",
    "rpc-password": "transmission",
    "rpc-authentication-required": true,
    "rpc-bind-address": "0.0.0.0",
    "rpc-port": 9091,
    "rpc-url": "/transmission/",
    "rpc-whitelist-enabled": true,
    "rpc-whitelist": "127.0.0.1,10.*.*.*",
}}}

Create a new FlexGet config.yml to specify your settings.  Change the download path, list of Series to download, and list of RSS feeds to download from.  Feel free to downgrade the or remove the quality setting from 720p to hdtv to capture standard-quality shows.  (It is highly recommend that you create the configuration file under the home path of a regular, non-root, user account for security reasons.)

'''~/.flexget/config.yml'''
{{{
presets:
  tv:
    private_torrents: no

    transmission:
      enabled: yes
      host: localhost
      port: 9091
      username: user
      password: transmission
      removewhendone: yes

    series:
      settings:
        tv:
          propers: 3 days
          min_quality: 720p
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
        - Office
        - Real Time with Bill Maher
        - South Park
        - True Blood
        - Weeds
        - Sons of Guns

feeds:
  bt-chat.com-tv:
    rss: http://rss.bt-chat.com/?group=3
    preset: tv

  ezrss.it:
    rss: http://ezrss.it/feed/
    preset: tv

  extratorrent.com-tv:
    rss: http://extratorrent.com/rss.xml?cid=8
    preset: tv

  kat.ph-tv:
    rss: http://kat.ph/tv/?rss=1
    preset: tv

  showrss.karmorra.info-tv:
    rss: http://showrss.karmorra.info/feeds/all.rss
    preset: tv

  thepiratebay.org-tv:
    rss: http://rss.thepiratebay.org/208
    preset: tv

  torrentz.eu-tv:
    rss: http://torrentz.eu/feed
    preset: tv
}}}

Use the command below to edit your crontab file for the user account where FlexGet will run so that it polls the RSS feeds hourly.

'''Commands - (As User)'''
{{{
crontab -e
}}}

Add line below to the user's crontab file.

{{{
@hourly /usr/local/bin/flexget --cron
}}}