= Installing !FlexGet in a virtualenv =

== What is virtual env ? ==

Virtual env is isolated Python environment. Libraries and applications inside it don't affect system installation in any way.

=== Create virtualenv ===

{{{
virtualenv ~/flexget/
}}}

=== Download !FlexGet egg ===

[[Include(http://download.flexget.com/ui/download.php)]]

And place it in virtualenv directory.

=== Install !FlexGet egg in virtualenv ===

Go into virtualenv directory and:

{{{
bin/easy_install FlexGet-1.0-py2.6.egg
}}}

This will install all required dependencies.

=== Running !FlexGet from virtualenv ===

In virtualenv directory:

{{{
bin/flexget [options]
}}}

== Continue ==

[wiki:InstallWizard/Linux/NoRoot/Virtualenv/Scheduling Scheduling]