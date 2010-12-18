== TODO: write instructions here ==

Wiki explaining installation [http://plugapps.com/index.php5?title=Application:Flexget here].

However it seems to discourage upgrading to Python 3 in !PlugBox. This shouldn't be a problem since you can install 2.x alongside 3.x just fine.

According to post [http://plugboxlinux.org/forum/viewtopic.php?f=9&t=368&start=10#p3071 here] the following should work fine if you are running Python 3.

{{{
pacman -S python2 python-distribute
easy_install-2.7 pip
pip install flexget
}}}

And to verify installation:

{{{
flexget -V
}}}