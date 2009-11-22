= Installing !FlexGet in a virtualenv =

== What is virtual env ? ==

Virtual env is isolated Python environment. Libraries and applications inside it don't affect system installation in any way.

=== Create virtualenv ===

{{{
virtualenv ~/flexget/
}}}

=== Activate virtualenv ===

{{{
source ~/flexget/bin/activate
}}}

=== Install !FlexGet egg in virtualenv ===

[[Include(http://download.flexget.com/ui/download.php)]]

Downloaded egg:

{{{
easy_install FlexGet-1.0-py2.6.egg
}}}

Or straight from the url:

{{{
easy_install http://download.flexget.com/unstable/FlexGet-1.0-py2.6.egg
}}}

This will install FlexGet and all required dependencies.

=== Running !FlexGet ===

You can either activate the virtualenv with the command:

{{{
source ~/flexget/bin/activate
}}}

After that command `flexget` works from anywhere. Or you can run it via:

{{{
~/flexget/bin/flexget [options]
}}}

== Continue ==

[wiki:InstallWizard/Linux/NoRoot/Virtualenv/Scheduling Scheduling]