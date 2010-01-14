= Exists =

Reject entries if same filename or directory already exists in given path (recursively).

== Example: ==

{{{
exists: /some/storage/path/
}}}

Multiple paths can be specified as a list:

{{{
exists:
  - /some/storage/path/
  - /another/storage/path/
}}}