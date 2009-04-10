= Operations =

All modules may do following operations to [wiki:Entry].

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
  <td><div style="color:#ff7300; font-weight: bold">Filter</div></td>
  <td>Entry will be marked implicitly removed. However it may still be Accepted or Rejected.</td>
</tr><tr>
  <td><div style="color:#97d000; font-weight: bold">None</div></td>
  <td>Entry is not marked to any category. Entry is implicitly accepted if nobody specifies anything.</td>
</tr>
</table>
}}}

== Examples ==

Assuming configuration:

{{{
regexp:
  accept:
    - Something
  filter:
    - XviD
  reject:
    - CAM
}}}

Q: What would happen to file '''Something.CAM.XviD'''[[BR]]
A: It would be rejected, since reject operation is stronger than accept.

Q: What would happen to file '''Something.XviD'''[[BR]]
A: It would be accepted, since filter operation is weaker.

