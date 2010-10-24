= Readynas !FlexGet installation =

This is just collected info from various sources and a bit of my own ideas. The guide will lead you through the installation of development files on your Readynas box to enable compilation of python and pysqlite which are necessary to install flexget on your Readynas machine.

= Requirements =

Basic linux knowledge you will need to access your readynas machine using a terminal program like [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html putty] Any ssh client will do though. Some spare time, compilation of the packages and libraries will take a few hours as the Readynas does not have a fast cpu on the spec list. This guide is simply a long list of commands you need to type in your terminal window (even better paste them in) To enable ssh access to your readynas visit this [http://www.readynas.com/?page_id=617 page] There you will also find APT support which will be needed.

= Set up environment =

{{{
apt-get update
apt-get install libc6-dev
apt-get install gcc
apt-get install libtag1-dev
apt-get install uuid-dev
apt-get install unrar unzip
apt-get install par2 parchive
apt-get install gpp
apt-get install libssl-dev
apt-get install zlibc
apt-get install zlib1g-dev

}}}

= Install Python 2.5 =

{{{
mkdir /c/src
cd /c/src
wget http://www.python.org/ftp/python/2.5.4/Python-2.5.4.tgz
gzip -d Python-2.5.4.tgz
tar xf Python-2.5.4.tar
cd Python-2.5.4
./configure --build=sparc-linux
make
make install
cd ..
}}}

= Fix missing local library =

When python is installed, I assume it is running the ldconfig command which will break most programs that reside in /usr/local/bin which is dependant from /usr/local/lib. It is because the readynas enviroment does not ship with a ld.so.conf file which tells the system where to look for libraries. This will take care of this.

{{{
echo /lib/ > /etc/ld.so.conf
echo /usr/lib >> /etc/ld.so.conf
echo /usr/local/lib >> /etc/ld.so.conf
ldconfig
}}}

= Install pysqlite =

{{{
wget http://pysqlite.googlecode.com/files/pysqlite-2.5.6.tar.gz
gzip -d -f pysqlite-2.5.6.tar.gz
tar xf pysqlite-2.5.6.tar
cd pysqlite-2.5.6
python setup.py build_static install
cd ..
}}}

= Install python easy_install =

{{{
wget http://peak.telecommunity.com/dist/ez_setup.py
python2.5 ez_setup.py
}}}

= Installing Flexget itself =

You could just head directly to [http://flexget.com/wiki/InstallWizard/Linux/Environment/FlexGet Link] Which is the generic linux installation page. Or read ahead for direct instructions:

{{{
easy_install flexget
}}}

= Verify flexget =

{{{
flexget -V
}}}

= Scheduling =

Scheduling on linux using crontab can be done in different ways. This is how i do ;-)

{{{
echo "*/30 * * * * /usr/local/bin/flexget" > /root/crontabfile
crontab /root/crontabfile
}}}

= Configuration =

!FlexGet is the most powerful downloader I have seen and can be tailored to do almost everything. But configuration is difficult the first time. Don't give up look at the examples and in 30 minutes you are able to write up your own powerful configuration :-) The official !FlexGet page has some good examples if you browse around a bit 
[http://flexget.com/wiki/Configuration]

!FlexGet by default tries to find it's configuration config.yml file in ~/.flexget/
I strongly encourage you to link that dir to the /c partition on your readynas device. The way !FlexGex operates it can use lots of space in the temp dir and you risk running out of space on the root file system which will cause bad things:

{{{
mkdir /c/flexget
ln -s /c/flexget/ /root/.flexget
}}}

This will ensure that flexget has enough space for even the most space demanding feeds :-)

= Final thoughts =

!FlexGet is a great tool for downloading files. Both torrents and podcasts and can really get anything you would like. With the built in prowl support you can have notifications sent directly to your iPhone. I have been using several tools to accomplish the same tasks but none of them worked really well. Flexget does and it comes in one package. I do recommend going through this guide and install it. It may look difficult but it really isn't. 

Running tools with your root account could lead to disaster. If you are really into security you should add a local user to run flexget.

= Configuration example =

{{{
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
    transmissionrpc:
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
}}}

This will use rss feed from [http://www.ezrss.it http://www.ezrss.it] and inject all episodes of Mythbusters, Csi and Fifth gear to a running [http://www.readynas.com/forum/viewtopic.php?f=47&t=24271 transmission] daemon. Path is set to series name to not clutter up your download directory. Use rss feed for the danish television DR2 and download all new episodes of a podcast show called So Ein Ding.

Thanks go out to [http://www.readynas.com/forum/viewtopic.php?f=36&t=41478 Meso_Tech] who wrote the thread on compiling and installing python on a readynas box and to [http://www.readynas.com/forum/viewtopic.php?f=36&t=42794#p257270 Riokmij]

Enjoy and happy downloading :-)
