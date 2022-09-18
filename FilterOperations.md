---
title: FilterOperations
description: 
published: true
date: 2022-09-18T04:49:33.484Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:49:30.771Z
---

# Actions
All plugins may do following actions (sometimes referred as operation) to [entry](/Entry).

* Accept
* Reject
* Fail

|State|Effect|
|---|---|
|Reject|Entry will be permanently removed. Other plugins may **not** change this status.|
|Accept|Entry will be marked accepted. Other plugins may still be reject it.|
|Failed|Entry was accepted and tried to be processed but an error prevented it being completed.|
|Undecided|Entry is not marked to any category _(default)_|


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