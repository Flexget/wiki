= Installing !FlexGet =

=== Install ===

Run command:

{{{
pip install flexget
}}}
or (from a normal user's shell)
{{{
sudo pip install flexget
}}}
{{{
Note: For Archlinux users pip refers to python3-pip. Use pip2 to install flexget as pip2 refers to python2-pip.
}}}
This will install !FlexGet and all additional components it requires.

If you get ''pip: command not found'' pip was not installed correctly in previous step.

=== Verify installation ===

Starting from this step, you shouldn't use root account for anything.

Run command:

{{{
flexget -V
}}}

== Continue ==

[wiki:InstallWizard/Linux/Environment/FlexGet/Scheduling Scheduling]