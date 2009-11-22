= Installing FlexGet Egg =

=== Download ===

Download !FlexGet 1.0 package, make sure to choose correct Python version:

[[Include(http://download.flexget.com/ui/download.php)]]

Save it somewhere temporarily, let's say `~/tmp/`

=== Install ===

Run command:

{{{
easy_install ~/tmp/<downloaded egg>
}}}

Example:

{{{
easy_install ~/tmp/FlexGet-1.0r963-py2.5.egg
}}}

This will install !FlexGet and all additional components it requires.

=== Verify installation ===

Starting from this step, you shouldn't use root account for anything.

Run command:

{{{
flexget -V
}}}

== Continue ==

[wiki:InstallWizard/Linux/Environment/FlexGet/Scheduling Scheduling]