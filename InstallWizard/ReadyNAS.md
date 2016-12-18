# Readynas FlexGet installation
17/12-2010:
This is second revision of the guide. Something did break and people had trouble getting sqlite support to work. This is tested on a readynas Duo box running Radiator 4.1.7 released November 12, 2010. This new release may have caused the breakage. I've removed some packages that is not used for this install. Warning, this is experimental at least. Use at your own risk :-)

This is just collected info from various sources and a bit of my own ideas. The guide will lead you through the installation of development files on your Readynas box to enable compilation of python and sqlite which are necessary to install flexget on your Readynas machine.

# Requirements
Basic linux knowledge you will need to access your readynas machine using a terminal program like [putty](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) Any ssh client will do though. Some spare time, compilation of the packages and libraries will take a few hours as the Readynas does not have a fast cpu on the spec list. This guide is simply a long list of commands you need to type in your terminal window (even better paste them in) To enable ssh access to your readynas visit this [page](http://www.readynas.com/?page_id=617) There you will also find APT support which will be needed.

# Set up environment
```
apt-get update
apt-get install libc6-dev gcc libtag1-dev libssl-dev zlibc zlib1g-dev

```

# Install sqlite
```
mkdir /c/src
cd /c/src
wget http://www.sqlite.org/sqlite-autoconf-3070400.tar.gz
tar xzf sqlite-autoconf-3070400.tar.gz 
cd sqlite-autoconf-3070400
./configure --build=sparc-linux
make install
cd ..
```

# Install Python 2.7.1
```
wget http://www.python.org/ftp/python/2.7.1/Python-2.7.1.tgz
tar xzf Python-2.7.1.tgz
cd Python-2.7.1
./configure --build=sparc-linux
make install
cd ..
```

# Fix missing local library
When python is installed, I assume it is running the ldconfig command which will break most programs that reside in /usr/local/bin which is dependant from /usr/local/lib. It is because the readynas enviroment does not ship with a ld.so.conf file which tells the system where to look for libraries. This will take care of this.

```
echo /usr/local/lib >> /etc/ld.so.conf
ldconfig
```

# Install Python setuptools
```
wget http://peak.telecommunity.com/dist/ez_setup.py
python ez_setup.py
```

# Installing Flexget itself
```
easy_install flexget
```


# Transmission support (optional)
```
easy_install transmissionrpc
```

# Verify flexget
```
flexget -V
```

# Scheduling
Scheduling on linux using crontab can be done in different ways. This is how i do ;-)

```
echo "*/30 * * * * /usr/local/bin/flexget" > /root/crontabfile
crontab /root/crontabfile
```

# Configuration
FlexGet is the most powerful downloader I have seen, and can be tailored to do almost everything. But configuration is difficult the first time. Don't give up look at the examples and in 30 minutes you are able to write up your own powerful configuration :-) The official FlexGet page has some good examples if you browse around a bit 
[https://flexget.com/wiki/Configuration](/https://flexget.com/wiki/Configuration)

FlexGet by default tries to find it's configuration config.yml file in ~/.flexget/
I strongly encourage you to link that dir to the /c partition on your readynas device. The way FlexGex operates it can use lots of space in the temp dir and you risk running out of space on the root file system which will cause bad things:

```
mkdir /c/flexget
ln -s /c/flexget/ /root/.flexget
```

This will ensure that flexget has enough space for even the most space demanding feeds :-)
8
# Configuration example
```
presets:
  global:
    prowl:
      apikey: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

  tv:
    series:
      - Mythbusters
      - Fifth gear
      - Csi
    set:
      path: /c/media/BitTorrent/%(series_name)s
    transmission:
      host: localhost
      port: 9091
      username: xxxxxxxxxxxx
      password: xxxxxxxxxxxx

  soeinding:
    download: /c/media/BitTorrent/SoEinDing

feeds:

  tv-shows:
    rss: http://www.ezrss.it/feed/
    preset: tv

  ding:
    rss: http://vpodcast.dr.dk/feeds/soeindingrss.xml
    preset: soeinding
    exists: /c/media/BitTorrent/SoEinDing/
```

This will use RSS feed from [http://www.ezrss.it](http://www.ezrss.it) and inject all episodes of Mythbusters, Csi and Fifth gear to a running [transmission](http://www.readynas.com/forum/viewtopic.php?f=47&t=24271) daemon. Path is set to series name to not clutter up your download directory. Use rss feed for the danish television DR2 and download all new episodes of a podcast show called So Ein Ding.

# Upgrading
FlexGet is in development and changes are frequent. If you ever need to update the script it is very simple. Issue this at the shell prompt:

```
easy_install --upgrade flexget
```

This will upgrade FlexGet. Visit https://flexget.com/wiki/UpgradeActions to see if any actions are needed to finish the upgrade.

# Feedback
Feedback can be directed to this thread: http://www.readynas.com/forum/viewtopic.php?f=35&t=48774

# Final thoughts
FlexGet is a great tool for downloading files. Both torrents and podcasts and can really get anything you would like. With the built in prowl support you can have notifications sent directly to your iPhone. I have been using several tools to accomplish the same tasks but none of them worked really well. FlexGet does and it comes in one package. I do recommend going through this guide and install it. It may look difficult but it really isn't. 

Running tools with your root account could lead to disaster. If you are really into security you should add a local user to run FlexGet.

Thanks go out to [Meso_Tech](http://www.readynas.com/forum/viewtopic.php?f=36&t=41478) who wrote the thread on compiling and installing python on a readynas box and to [Riokmij](http://www.readynas.com/forum/viewtopic.php?f=36&t=42794#p257270)

Enjoy and happy downloading :-)
