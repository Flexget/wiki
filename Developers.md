= How to make custom modules =

Making custom modules should be easy for anyone with some python experience.

Each module file must have one special variable set, called {{{__instance__}}}. This will tell what class is to be instantiated from module.
Instantiated class must have method with following signature:

{{{
def register(self, manager):
}}}

!FlexGet calls this method after instance has been created. From this method module may register itself roles in which it wishes to function.
Currently available roles are start, input, filter, download, modify, output and exit. In practice this is only order where modules are executed.

To register module you must call {{{manager.register}}}, which accepts named arguments.

{{{
Mandatory arguments:
    instance    - instance of module (self)
    keyword     - maps directly into config
    callback    - method that is called when module is executed
    type        - specifies when module is executed and implies what it does
Optional arguments:
    order       - when multiple modules are enabled this is used to
                  determine execution order. Default 16384.
    builtin     - set to True if module should be executed always
}}}

Example:
{{{
  manager.register(instance=self, keyword='ourtest', callback=self.execute, type='filter')
}}}

Now when keyword {{{ourtest}}} is found from feed configuration, callback method is executed. The callback method must have following signature:

{{{
def execute(self, feed):
}}}