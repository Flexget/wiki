= Some sketches for api_ver 3 =

We're planning to move away from task.entries and instead pass iterable to the plugin, new method signature will be:

{{{
def on_task_xxx(self, task, config, entries):
}}}

== Iterating entries ==

This is still the open question.

=== Option 1 - helpers ===

{{{
from flexget.entry import accepted, rejected, undecided

# and then iterating
for entry in accepted(entries):
  pass

}}}

* Old task.entries contained undecided AND accepted, how would this be with the new system? Default entries implicitly to accepted and undecided? Not very obvious!
* Requires imports

=== Option 2 - generator expression ===

{{{
for entry in (e.accepted for e in entries):
  e.reject()
}}}

* Slightly more verbose
* Feels very pythonic and is very explicit
* Iterating the old task.entries is even more verbose - and we do this most

{{{
for entry in (e.accepted or e.undecided for e in entries):
  e.reject()
}}}
