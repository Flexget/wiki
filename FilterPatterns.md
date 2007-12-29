= Patterns =

Filter out [wiki:entry entries] based on regular expression matches.
Configuration example:

{{{
patterns:
  - regular expression
  - another reqular expression
}}}

== Advanced users: ==

It's also possible to specify custom download path for
pattern and secondary regexp(s) that causes entry to be
filtered even when primary regexp matches entry.

Examples:

{{{
pattenrs:
  # simplest way to specify custom path
  - regexp1: ~/custom_path/

  # alternative way to specify custom path
  - regexp2:
      path: ~/custom_path/

  # specify custom path and secondary single filter regexp
  - regexp2:
      path: ~/custom_path/
      not: regexp3

  # multiple secondary filter regexps
  - regexp4:
      not:
        - regexp5
        - regexp6

  # Tip: In yaml you can write dictionaries and lists in inline form.
  # Above examples can be written also as:
  - regexp2: {path: ~/custom_path/, not: regexp3}
  - regexp4: {not: [regexp5, regexp6]}
}}}