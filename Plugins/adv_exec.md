# Advanced exec
**As of r1552 adv_exec has become [exec plugin advanced configuration](/Plugins/exec#AdvancedConfiguration).**

Execute commands.

**Format:**

```
adv_exec:
  [ON_EVENT](/ON_EVENT):
    [event](/event): CMD
    [FOR_ENTRIES](/FOR_ENTRIES): CMD
```

Available *ON_EVENTS*: on_start, on_input, on_filter, on_output and on_exit
  
Available *FOR_ENTRIES*: for_entries, for_accepted and for_rejected
  
  
    
**Example:**

```
adv_exec: 
  on_start: 
    event: echo "Started"
  on_input:
    for_entries: echo 'got %(title)s'
  on_output: 
    for_accepted: echo 'accepted %(title)s - %(url)s' > file
```
    
You can use all (available) entry fields in the command. If you would like an entry to fail if entry field is not available, you can set the fail_entries option to yes, like this:

```
adv_exec:
  fail_entries: yes
  on_output: 
    for_accepted: echo 'accepted %(title)s - %(url)s' > file
```

Setting the fail_entries option to yes will also cause the entry to fail if the executed command has a non-zero return code.