= Install EGG on windows =

=== Download ===

Download !FlexGet package, make sure to choose correct Python version:

[[Include(http://download.flexget.com/ui/download.php)]]

Store it somewhere temporarily, let's say `c:\`

=== Install ===

Run command:

{{{
easy_install c:\<downloaded egg>
}}}

Example:

{{{
easy_install c:\FlexGet-1.0r963-py2.5.egg
}}}

This will install !FlexGet and all the dependencies.

=== Verify installation ===

Run command:

{{{
flexget -V
}}}

It should verbose the installed version.

== Next step ==

[wiki:InstallWizard/Windows/Egg/Schedule Scheduling]

