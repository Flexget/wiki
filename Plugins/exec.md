= Exec = 

Executes commands on [wiki:Entry entries].

This plugin can take two configuration formats [#SimpleConfiguration simple] and [#AdvancedConfiguration advanced].

== Simple Configuration ==

With this configuration, your command is executed on all accepted entries that reach output.

=== Example ===

{{{
exec: echo "found %(title)s at %(url)s" >> file
}}}

=== Example 2 ===

{{{
exec: echo "downloaded file %(output)s" >> file
}}}


You can use all (available) [wiki:Entry entry] fields in the command.

== Advanced Configuration^^^*^^^ ==

If you need more control over what entries and when the command gets executed, you can use the advanced configuration format. This requires some understanding of how the [wiki:Developers internals] of !FlexGet work.

Execute commands.

'''Format:'''

{{{
exec:
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
exec: 
  on_start: 
    event: echo "Started"
  on_input:
    for_entries: echo "got %(title)s"
  on_output: 
    for_accepted: echo "accepted %(title)s - %(url)s" > file
}}}
    
See [wiki:Entry entry documentation] for list of possible fields.

=== Fail entries option ===
Setting the {{{fail_entries}}} option to yes will cause the entry to fail if the executed command has a non-zero return code.
This option will also cause entries to fail that do not contain all of the variables needed for string substitution.
{{{
exec:
  fail_entries: yes
  on_output: 
    for_accepted: echo "accepted %(title)s - %(url)s" > file
}}}

=== Auto escape option ===

If one of your variables may contain characters that need to be escaped for the shell, you can use the {{{auto_escape}}} option. This will escape all non-word characters with backslash before doing string substitution. For example:
{{{
exec:
  auto_escape: yes
  on_output: 
    for_accepted: echo accepted\ %(title)s\ -\ %(url)s > file
}}}

^^^* Prior to r1552 advanced configuration was it's own plugin, adv_exec.^^^