= Configuration =

First, you need to create a different yaml configuration for
this. This is necessary because the series might be duplicate from the
series torrents download. We will call it 'subs-config.yml'.

This is the content of my subs-config.yml

{{{
feeds:
  series-subs:
    text:
      url: http://api.twitter.com/1/statuses/user_timeline.rss?screen_name=legendas
      entry:
        title: <title>legendas. Legenda ([^ ]*).*
        url: (http\://t.co/[^<]*)</title>
    manipulate:
      - title:
          replace:
            regexp: '[\.-]'
            format: ' '
    series:
      - south park
      - house
      - how i met your mother
      - family guy
      - the big bang theory
      - crime scene investigation
      - csi
      - futurama
      - burn notice
      - the cleveland show
    download:
      path: /home/torrents/.flexget/subs-temp
      fail_html: no
    exec: 
      auto_escape: yes
      fail_entries: yes
      on_output:
        for_accepted: /home/torrents/.flexget/download-sub.sh {{url}}
    email:
      from: email-from@host
      to: email-to@host
      smtp_host: smtp.gmail.com
      smtp_port: 587
      smtp_username: username
      smtp_password: password
      smtp_tls: yes
}}}

What we do here is that we download the rss from legendastv twitter
and separate the entries regexp'ing their titles and the description
content for the URL we're looking for. The URL is minimized with
http://t.co service. We also replace all points and minus for space
for better legibility.

We use the series plugins which is episode-aware and other goodies
to select which series subtitles we want to download. We then
ask to download it so the email plugin works OK. And we execute
a script which will actually download the subtitle.

Why do we need a script to download you may ask. The truth is the
URL we get by the RSS in twitter doesn't point directly to
the subtitle file. But to a page with a Download button. This
page will only appear this way if you are logged in to legendas.tv
site. If you don't have a login and username, create one because
you'll need it.

Mine download-sub.sh uses wget and other Linux utilities to download,
so you may have a hard time using it under Windows, though cygwin
might help you there. Here it is download-sub.sh:

{{{
#!/bin/bash

echo Logging in

LOGIN=mylogin
PASSWORD=mypassword

/usr/bin/wget --keep-session-cookies --base http://legendas.tv --user-agent="Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)" --referer http://legendas.tv --save-cookies=/home/torrents/.flexget/login.txt --post-data="&a=post&txtLogin=$LOGIN&txtSenha=$PASSWORD&chkLogin=1" http://legendas.tv/login_verificar.php -O /dev/null &> /dev/null

if [ "$?" -ne "0" ]; then
    echo "Wget returned code $?"
    exit 1
fi

echo Downloading URL $1

SUBURL=`/usr/bin/wget --load-cookies /home/torrents/.flexget/login.txt $1 -O /dev/null |& sed -n "s/Location: \(\/info\.php?d=[a-z0-9A-Z]*\).*/http:\/\/legendas.tv\1\&c=1/ p"`

if [ "$?" -ne "0" ]; then
    echo "Wget returned code $?"
    exit 1
fi

echo SUBURL: $SUBURL

if [ -z "$SUBURL" ]; then
    echo "sed'ed SUBURL is invalid (empty)"
    exit 1
fi

echo Downloading $SUBURL

RANDOMFILE=subtitle_$RANDOM

SUBNAME=`/usr/bin/wget --load-cookies /home/torrents/.flexget/login.txt $SUBURL -O ~/.flexget/subs-temp/$RANDOMFILE |& sed -n "s/^Location: legenda[^\/]*\/\([^ ]*\).*/\1/ p"`

if [ "$?" -ne "0" ]; then
    echo "Wget returned code $?"
    exit 1
fi

if [ -z "$SUBNAME" ]; then
    echo "sed'ed SUBNAME is invalid (empty)"
    exit 1
fi

echo Renaming to $SUBNAME

mv /home/torrents/.flexget/subs-temp/$RANDOMFILE /home/torrents/torrents-storage/series/Legendas/$SUBNAME

if [ "$?" -ne "0" ]; then
    echo "mv returned code $?"
    exit 1
fi

exit 0
}}}


Which downloads the subtitle and moves it to
/home/torrents/torrents-storage/series/Legendas/NAME with the name of
the file from legendas.tv page. If you want it to use a better name,
you can change the last step "Renaming".

You will then need to call 'flexget -c subs-config.yml' to download the subtitles,
and don't forget --cron if you register it in crontab.

Hope this helps,

Regards,


Felipe Magno de Almeida
