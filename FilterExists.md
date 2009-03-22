= Exists =

Reject entries if same filename or directory already exists in given path (recursively).

== Example: ==

{{{
exists: /some/storage/path/
}}}

And must be under global if several feeds are used and you want it the work on all feeds.
== Example: ==

{{{
Global:
  exists: /some/storage/path/
  exists: /some/storage/path/
}}}