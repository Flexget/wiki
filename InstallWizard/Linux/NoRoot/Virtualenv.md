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

[[Include(wiki:InstallWizard/Partial/InstallVirtualenv)]]

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