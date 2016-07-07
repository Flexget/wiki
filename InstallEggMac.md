# If installing the egg fails (mac 10.6)
You will need to install FlexGet from source distribution (poorly available, atm) and handle dependencies manually.

Installing from [subversion](/Subversion) might work too.

To to install the dependencies you can do:

```
sudo easy_install FeedParser && sudo easy_install SQLAlchemy && sudo easy_install PyYAML && sudo easy_install BeautifulSoup && sudo easy_install html5lib
```

and to install, you can do:

```
cd /path/to/source/ && python setup.py install
```

(where /path/to/source/ is the UNIX paths location of the unarchived soucre (eg: ~/downloads/FlexGet-x.xxx) use `tar -xzvf FlexGet-x.xxx.tar.gz` to extract)