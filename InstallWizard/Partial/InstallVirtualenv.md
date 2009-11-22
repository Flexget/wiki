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

This will install !FlexGet and all the required dependencies.

=== Running !FlexGet from the virtualenv ===

You can either activate the virtualenv with the command:

{{{
source ~/flexget/bin/activate
}}}

After that command `flexget` works from anywhere. Or you can run it via:

{{{
~/flexget/bin/flexget [options]
}}}

