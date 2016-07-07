# Operations
All plugins may do following operations to [entry](/Entry).


<table class="wiki">
<tr>
  <td><strong>Operation</strong></td>
  <td><strong>Effect</strong></td>
</tr><tr>
  <td><div style="color:red; font-weight: bold">Reject</div></td>
  <td>Entry will be permanently removed. Other plugins may not change this status.</td>
</tr><tr>
  <td><div style="color:green; font-weight: bold">Accept</div></td>
  <td>Entry will be marked accepted. Other plugins may still be reject it.</td>
</tr><tr>
  <td><div style="color:#666; font-weight: bold">Undecided</div></td>
  <td>Entry is not marked to any category <i>(default)</i></td>
</tr>
</table>


### Represented as a schematic
<img src="/attachments/FilterOperations/1.0_operations.png">

## Scenario
Assuming configuration:

```
regexp:
  accept:
    - Something
  reject:
    - CAM
```

Q: What would happen to file **Something.CAM.XviD**  
A: It would be rejected, since reject operation is stronger than accept.

Q: What would happen to file **Something.XviD**  
A: It would be accepted

Q: What would happen to file **Example.XviD**  
A: It wouldn't be intervened any way, neither accepted nor rejected. Note that output plugins are interested only in accepted entries.

### Attachments
* [describe operations in 0.9](/attachments/FilterOperations/0.9_operations.png)
* [1.0 operations](/attachments/FilterOperations/1.0_operations.png)