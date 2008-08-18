= Filter operations =

Modules may do following operations to [wiki:Entry].

{{{
#!html
<table class="wiki">
<tr>
  <td><strong>Operation</strong></td>
  <td><strong>Effect</strong></td>
</tr><tr>
  <td><div style="color:red; font-weight: bold">Reject</div></td>
  <td>Entry will be removed. Other modules may not change this status.</td>
</tr><tr>
  <td><div style="color:green; font-weight: bold">Accept</div></td>
  <td>Entry will be marked accepted. Filtering this entry has no effect. May still be Rejected.</td>
</tr><tr>
  <td><div style="color:#ff6000; font-weight: bold">Filter</div></td>
  <td>Entry will be marked implicitly removed. However it may still be Accepted or Rejected.</td>
</tr><tr>
  <td><div style="color:#ffcc00; font-weight: bold">None</div></td>
  <td>Entry is not marked to any category. Entry is implicitly accepted if nobody specifies anything.</td>
</tr>
</table>
}}}


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
