= Set up environment =

== Python ==

Start by making sure you have Python '''2.6.x - 2.7.x''' available. Try running commands:

{{{
python -V
}}}

In some distributions the newer python may be available trough commands:

{{{
python26 -V
python27 -V
}}}

If you don't have required version already available, install it from your distribution package manager.

With Debian based distributions you can simply run with root privileges:

{{{
sudo apt-get install python2.7
}}}

With Arch Linux based distributions you can simply run with root privileges:

{{{
sudo pacman -S python2
}}}

== pip ==

If you do not have `pip` already available, you need to install it.

With Debian based distributions you can simply run with root privileges:

{{{
sudo apt-get install python-pip
}}}

With Arch Linux based distributions you can simply run with root privileges:

{{{
sudo pacman -S python2-pip
}}}

If your distribution does not have the package available, see further instructions from 

[http://www.pip-installer.org/en/latest/installing.html#using-the-installer]

= Next =

[wiki:InstallWizard/Linux/Environment/FlexGet Install FlexGet]