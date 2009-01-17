= Release changes =

If you're old !FlexGet user using subversion or cookbook example to download latest releases this contains some important information.

== Subversion checkout from trunk ==

Subversion trunk will be used to develop application, meaning that it is likely somewhat unstable. More troublesome is the fact that there is going to be changes affecting session storage. This will result loss of session information and re-downloads unless you stay sharp, keep eye on svn log and use --learn when suggested.

You should switch to 0.9 branch if you want trouble free operation.

'''Command:'''

{{{
svn switch http://svn.flexget.com/branches/0.9
}}}

If you want to be bleeding edge beta tester feel free to switch or stay on trunk. Remember to report any problems you encounter.

== Cook book recipe ==

If you're using cook book example that downloads latest !FlexGet builds it will no longer work. Update your configuration to revised recipe.