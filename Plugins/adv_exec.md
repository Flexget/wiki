= Advanced exec =

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
    for_accepted: echo 'accepted %(title)s - %(url)s > file
}}}
    
You can use all (available) entry fields in the command.
