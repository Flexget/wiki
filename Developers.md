= How to make custom modules =

'''API is not yet stabilized. Expect some changes to happen. Yes, documentation is a bit messy ...'''

Making custom modules should be easy for anyone with some python experience.

If you have good re-usable module under construction I'd be more than happy to include it in official distribution. [wiki:Contact] me for subversion write permissions.

Each module must have at least one '''unique''' class with register method with following signature:

{{{
def register(self, manager, parser):
}}}

!FlexGet creates instance of this class and calls the register method. From this method module may register itself.

To register your module call {{{manager.register}}}. You must at least specify module name:

{{{
manager.register('new')
}}}

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

 cache::
  '''will be gone in 1.0''' Cache class for storing persistent information, this is unique for each feed.

 shared_cache::
  '''will be gone in 1.0''' Cache class for storing persistent information, this is not feed specific.

 entries::
  list containing [wiki:DevelopersEntry entries].

You shouldn't modify name or config as they are used by other modules.

=== Available methods: ===

 accept(entry, [reason])::
  Mark entry accepted, filtering this later do not affect status. Call this on entries module knows should be downloaded.

 filter(entry, [reason])::
  Mark entry to be filtered, other modules may still however accept entry.

 reject(entry, [reason])::
  Mark entry to be removed. It will be removed from feed once module event returns.

 failed(entry)::
  Mark entry to be failed (download)

 get_failed_entries()::
  Return set containing all failed entries.

 get_succeeded_entries()::
  Return set containing all succeeded entries.

 get_input_url(keyword)::
  Helper method for modules. Return url for a specified keyword.
  Supports configuration in following forms:[[BR]]
  ..<keyword>: <address>[[BR]]
  and[[BR]]
  ..<keyword>:[[BR]]
  ....url: <address>
  '''Will be moved in 1.0'''

== Cache class ==

  '''Will be removed in 1.0'''

  store(key, value, days=30)::
    Stores key value pair for number of days. Value must be yaml compatible. Default number of days is 30.

  storedefault(key, value, default, days=30)::
    Similar to dictionary setdefault.

  get(key, default=None)::
    Get stored value, passed default (or None) if not found.

== Manager class ==

  Accessible trough feed.manager

  get_module_by_name(name)

  get_modules_by_group(group)

  unit_test::
    True when executing unit tests