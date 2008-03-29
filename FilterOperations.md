= Filter operations =

Modules may do following operations to [wiki:Entry].

||'''Operation'''||'''Effect'''||
||Accept||Entry will be marked explicitly accepted. Filtering this entry has no effect.||
||Filter||Entry will be marked implicitly removed. However it may still be Accepted or Rejected.||
||Reject||Entry will be removed. Other modules may not change this status.||
||<none>||Entry is not marked to any above categories. Entry is implicitly accepted.||

== Examples ==

Assuming configuration:

{{{
ignore:
  - CAM
patterns:
  - XviD
}}}

And if we encounter file named: '''Something.CAM.XviD'''[[BR]]
Q: What would happend?[[BR]]
A: Module patterns would mark it '''accepted''', but later module ignore would mark it as '''rejected'''.
