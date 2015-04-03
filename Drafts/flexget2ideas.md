= Ideas for larger changes that may come with flexget 2 =

All input on any of these ideas is welcome.

=== Plugins ===

Problem: Right now, we have one mount point for plugins, and keep track of which interface they use by the 'groups' attribute of the plugin. Some plugins don't even register to that mount point (scheduler, api_tvdb) and work totally based on hooks or explicit calls.

Better ways?: http://martyalchin.com/2008/jan/10/simple-plugin-framework/ This describes a very simple framework where it is easy to register and keep track of plugins at various mount points. It would also make it very easy for a plugin itself to define a new mount point for plugins. Mountpoints I would imagine having in this system: processor plugins (the ones that go in tasks), thread plugins (like scheduler), search plugins, urlrewrite plugins, (and probably more.) The class for each of these would be an easy place to document what the interface for interacting with each of these types of plugins was (whereas right now there is no clear place to document interfaces for things like search or urlrewrite plugins.)


