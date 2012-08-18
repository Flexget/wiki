'''{{{This page needs updated to use python 2.6 or 2.7 (and preferably pip.) Please feel free to do so.}}}'''
= TODO: write =

{{{
ipkg install py25-setuptools
easy_install flexget
}}}

This should work, but for some it doesn't.

If you're low on disk space on root try [wiki:Subversion subversion route].

See forum thread [http://forum.qnap.com/viewtopic.php?f=16&t=24864 here]

On some systems the /tmp folder is not big enough to allow the installation to complete. You can temporarily make it bigger by executing:
{{{
mount -oremount,size=128M /tmp
}}}