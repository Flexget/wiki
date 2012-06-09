= Installing !FlexGet in a virtualenv =

== What is virtual env ? ==

Virtual env is isolated Python environment. Libraries and applications inside it don't affect system installation in any way.

=== Create virtualenv ===

{{{
virtualenv ~/flexget/
}}}

'''Note:''' if you plan to use the [wiki:Plugins/deluge deluge] plugin, you need to build your virtualenv with the --system-site-packages option: {{{virtualenv --system-site-packages ~/flexget/}}}

[[Include(wiki:InstallWizard/Partial/InstallVirtualenv)]]

== Continue ==

[wiki:InstallWizard/Linux/NoRoot/Virtualenv/Scheduling Scheduling]