= Tough luck =

You must install and compile all required dependencies into your home directory.

== Installing Python ==

Download Python 2.6 package from [http://www.python.org/] (source distribution)

Download and extract it:

{{{
wget http://www.python.org/ftp/python/2.6.3/Python-2.6.3.tar.bz2
tar xjf Python-2.6.3.tar.bz2
}}}

Compile:

{{{
cd Python-2.6.3
./configure --prefix=$HOME/python
make
make install
}}}

{{{
Failed to find the necessary bits to build these modules:
_bsddb             _sqlite3           _tkinter
bsddb185           bz2                dbm
gdbm               readline           sunaudiodev
To find the necessary bits, look in setup.py in detect_modules() for the module's name.
}}}

'''TODO: how to resolve these, at least _sqlite is needed! '''

New Python should be now executable with {{{~/python/bin/python}}}, which you can easily add to your .bashrc

{{{
alias python2.6='~/python/bin/python'
}}}

After relogin `python2.6` should work nicely for !FlexGet.

== Continue ==

''todo: link''