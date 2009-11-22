= Install Egg on windows =

=== Download ===

Download !FlexGet 1.0 package, make sure to choose correct Python version:

[[Include(http://download.flexget.com/ui/download.php)]]

Save it somewhere temporarily, let's say `c:\tmp\`

=== Install ===

Run command:

{{{
easy_install c:\tmp\<downloaded egg>
}}}

Example:

{{{
easy_install c:\tmp\FlexGet-1.0r963-py2.5.egg
}}}

This will install !FlexGet and all additional components it requires.

=== Verify installation ===

Run command:

{{{
flexget -V
}}}

It should verbose the installed version. When you've reached this step you have already application running properly.

== Continue ==

After you've verified !FlexGet installation.

[wiki:InstallWizard/Windows/Egg/Scheduling Scheduling]

