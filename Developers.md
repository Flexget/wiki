[[PageOutline]]

= How to make custom plugins (bleeding edge) =

'''API is not yet stabilized. Expect some changes to happen. Yes, documentation is a very messy ... feel free to improve'''

Resources:

 * [wiki:HowToTDD test driven development how to]
 * [http://coverage.flexget.com unit test coverage]
 * [http://doc.flexget.com generated documents] ''not yet up(?)''

Making custom plugins should be easy for anyone with some python experience.

If you're working on good re-usable plugin I'd be more than happy to include it in official distribution. [wiki:Contact] me for subversion write permissions.

== Registering plugins ==

Plugins are registered by calling {{{register_plugin}}} method.

{{{
register_plugin(<class name>, '<keyword>', [parameters])
}}}

You can also pass some optional named arguments

{{{
Optional arguments:
    priority    - when multiple plugins of same event type are enabled for a feed
                  this is used to determine execution order. Default 0. Larger number, higher priority.
    builtin     - set to True if plugin should be executed always
    group       - group name this plugin belongs to
    groups      - list of group names this plugin belongs to
}}}

Example:
{{{
register_plugin(FilterRegexp, 'regexp', priorities={'filter': 128})
}}}

=== Event methods ===

Listed in order of execution.

 * on_feed_start(self, feed)
 * on_feed_input(self, feed)
 * on_feed_filter(self, feed)
 * on_feed_download(self, feed)
 * on_feed_modify(self, feed)
 * on_feed_output(self, feed)
 * on_feed_exit(self, feed)

''TODO: explain event roles? on start and exit there is no feed.session!''

=== Registering custom events ===

Plugins may create new feed events, signature is on_feed_<name>(self, feed).

=== Application events ===

 * on_process_start(self, feed)
 * on_process_end(self, feed)

These are triggered on startup and shutdown, not between feeds.

=== Adding commandline parameters ===

You can also add more commandline parameters. Check existing plugins. See [http://optik.sourceforge.net/ Optik homepage] for documentation.

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

 simple_persistence::
  provides easy key, value persistence for modules that do not require the full SQLAlchemy capabilities.

You shouldn't modify name or config as they are used by other modules.

=== Feed methods ===

 accept(entry, [reason])::
  Mark entry accepted. Can still be rejected

 reject(entry, [reason])::
  Mark entry to be removed. It will be removed from feed once module event returns.

 fail(entry)::
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

== Running IPython inside FlexGet ==

{{{
from IPython.Shell import IPShellEmbed
ipshell = IPShellEmbed()
ipshell()
}}}