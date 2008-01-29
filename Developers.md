= How to make custom modules =

'''API is not yet stabilized. Expect some changes to happen.'''

Making custom modules should be easy for anyone with some python experience.

If you have good re-usable module under construction I'd be more than happy to include it in official distribution. [wiki:Contact] me for subversion write permissions.

Each module must have at least one '''unique''' class with register method with following signature:

{{{
def register(self, manager, parser):
}}}

!FlexGet creates instance of this class and calls the register method. From this method module may register itself events in which it wishes to function and add new commandline parameters. Currently available events are start, input, filter, download, modify, output and exit.

To register module you must call {{{manager.register}}}, which accepts named arguments.

{{{
Mandatory arguments:
    instance    - instance of module (self)
    keyword     - maps directly into config
    callback    - method that is called when module is executed
    event       - specifies when module is executed and implies what it does
Optional arguments:
    order       - when multiple modules are enabled this is used to
                  determine execution order. Default 16384.
    builtin     - set to True if module should be executed always
}}}

Example:
{{{
  manager.register(instance=self, keyword='ourtest', callback=self.execute, event='filter')
}}}

Now when keyword {{{ourtest}}} is found from feed configuration, callback method is executed. The callback method must have following signature:

{{{
def execute(self, feed):
}}}

=== Adding commandline parameters ===

In register you can also add more commandline parameters, parser parameter is Optik class that has simple method for adding parameters. See [http://optik.sourceforge.net/ Optik homepage] for documentation.

== Feed class ==

Feed is a class that represents one feed in configuration file.

=== It has following attributes: ===

 name::
  name of the feed

 config::
  feed specific configuration (dict).

 cache::
  Cache class for storing persistent information, this is unique for each feed.

 shared_cache::
  Cache class for storing persistent information, this is not feed specific.

 entries::
  list containing [wiki:Entry entries].

 last::
  True if this is last feed that !FlexGet will execute.

You shouldn't modify name or config as they are used by other modules.

=== Available methods: ===

 accept(entry)::
  Mark entry accepted, filtering this later do not affect status. Call this on entries module knows should be downloaded.

 filter(entry, [immediately])::
  Mark entry to be filtered, other modules may still however accept entry.
  If optional immediately is set to True this entry is removed from entries unconditionally asap. 
  Use this flag on entries that module has determined that should not be downloaded never, ie. previously already downloaded.

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

== Cache class ==

  store(key, value, days=30)::
    Stores key value pair for number of days. Value must be yaml compatible. Default number of days is 30.

  storedefault(key, value, default, days=30)::
    Similar to dictionary setdefault.

  get(key, default=None)::
    Get stored value, passed default (or None) if not found.