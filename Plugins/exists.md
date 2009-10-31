= Exists =

Reject entries if same filename or directory already exists in given path (recursively).
Also series aware and will reject entries that have the same series identifier and quality as a file in given path.

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