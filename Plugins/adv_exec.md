---
title: adv_exec
description: 
published: true
date: 2022-09-18T05:01:50.046Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:01:47.534Z
---

= Advanced exec =

'''As of r1552 adv_exec has become [wiki:Plugins/exec#AdvancedConfiguration exec plugin advanced configuration].'''

Execute commands.

'''Format:'''

{{{
adv_exec:
  [ON_EVENT]:
    [event]: CMD
    [FOR_ENTRIES]: CMD
}}}

Available ''ON_EVENTS'': on_start, on_input, on_filter, on_output and on_exit
[[BR]]
Available ''FOR_ENTRIES'': for_entries, for_accepted and for_rejected
[[BR]]
[[BR]]
    
'''Example:'''

{{{    
adv_exec: 
  on_start: 
    event: echo "Started"
  on_input:
    for_entries: echo 'got %(title)s'
  on_output: 
    for_accepted: echo 'accepted %(title)s - %(url)s' > file
}}}
    
You can use all (available) entry fields in the command. If you would like an entry to fail if entry field is not available, you can set the fail_entries option to yes, like this:

{{{
adv_exec:
  fail_entries: yes
  on_output: 
    for_accepted: echo 'accepted %(title)s - %(url)s' > file
}}}

Setting the fail_entries option to yes will also cause the entry to fail if the executed command has a non-zero return code.