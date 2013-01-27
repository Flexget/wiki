= Sort By =

Sorts task entries in order by [wiki:Entry#Knownfields field]. Useful for generating RSS in particular order.

=== Example ===

{{{
sort_by: title
}}}

If you need to reverse the order of the sort, use this format:

{{{
sort_by:
  field: imdb_score
  reverse: yes
}}}