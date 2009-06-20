= How to make custom plugins (bleeding edge) =

'''API is not yet stabilized. Expect some changes to happen. Yes, documentation is a very messy ... feel free to improve'''

Making custom modules should be easy for anyone with some python experience.

If you have good re-usable module under construction I'd be more than happy to include it in official distribution. [wiki:Contact] me for subversion write permissions.

''todo: write about registering a plugin''

You can also pass some optional named arguments

{{{
Optional arguments:
    priority    - when multiple modules of same event type are enabled for feed
                  this is used to determine execution order. Default 0. Larger number, higher priority.
    builtin     - set to True if module should be executed always
    group       - group name this module belongs to
    groups      - list of group names this module belongs to
}}}

Example:
{{{
  manager.register('new', priority=2)
}}}

Now when keyword {{{new}}} is found from feed configuration, event methods are called.

=== Event methods (in order): ===

 * feed_start(self, feed)
 * feed_input(self, feed)
 * feed_filter(self, feed)
 * feed_download(self, feed)
 * feed_modify(self, feed)
 * feed_output(self, feed)
 * feed_exit(self, feed)

Modules may create new events, signature is in form of feed_<name>(self, feed).

''TODO: explain event roles?''

=== Application events ===

 * application_terminate(self, feed)

=== Adding commandline parameters ===

In register you can also add more commandline parameters, parser parameter is Optik class that has simple method for adding parameters. See [http://optik.sourceforge.net/ Optik homepage] for documentation.

== Feed class ==

Feed is a class that represents one feed in configuration file.

=== Feed's attributes: ===

 name::
  name of the feed

 config::
  feed specific configuration (dict).

 entries::
  list containing [wiki:DevelopersEntry entries].

 accepted::
  list containing accepted entries

 rejected::
  list containing rejected entries

You shouldn't modify name or config as they are used by other modules.

=== Available methods: ===

 accept(entry, [reason])::
  Mark entry accepted. Can still be rejected

 reject(entry, [reason])::
  Mark entry to be removed. It will be removed from feed once module event returns.

 failed(entry)::
  Mark entry to be failed (ie. download 404 etc)

 get_input_url(keyword)::
  Helper method for modules. Return url for a specified keyword.
  Supports configuration in following forms:[[BR]]
  ..<keyword>: <address>[[BR]]
  and[[BR]]
  ..<keyword>:[[BR]]
  ....url: <address>
  '''Will be moved in 1.0'''

== Manager class ==

  Accessible trough feed.manager

  unit_test::
    True when executing unit tests

== Plugin class ==

''todo: write ''

== Unit testing ==

=== Run tests ===

{{{
bin/paver test
}}}

Argument {{{--online}}} can be used to enable online tests

=== Run a single test ===

{{{
bin/nosetests tests/__init__.py:TestDisableBuiltins
}}}