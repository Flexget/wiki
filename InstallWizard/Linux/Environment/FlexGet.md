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

This will install !FlexGet and all additional components it requires.

In some cases, your system might says ''pip: command not found''. In that case, try to run:

{{{
pip2 install flexget
}}}
or (from a normal user's shell)
{{{
sudo pip2 install flexget
}}}

=== Verify installation ===

Starting from this step, you shouldn't use root account for anything.

Run command:

{{{
flexget -V
}}}

== Continue ==

[wiki:InstallWizard/Linux/Environment/FlexGet/Scheduling Scheduling]