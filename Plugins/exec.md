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

== Advanced Configuration^^^1, 2^^^ ==

If you need more control over what entries and when the command gets executed, you can use the advanced configuration format. This requires some understanding of how the [wiki:Developers internals] of !FlexGet work.

Execute commands.

'''Format:'''

{{{
exec:
  [ON_PHASE]:
    [phase]: CMD
    [FOR_ENTRIES]: CMD
}}}

Available ''ON_PHASE'': on_start, on_input, on_filter, on_output and on_exit
[[BR]]
Available ''FOR_ENTRIES'': for_entries, for_accepted, for_rejected and for_failed
[[BR]]
[[BR]]
    
'''Example:'''

{{{    
exec: 
  on_start: 
    phase: echo "Started"
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

=== Allow background option ===

Normally, !FlexGet will wait the given command to finish so it can capture the return status and log the output. But if the command takes a long time to run (ex. direct downloads of large files), it will prevent further processing until the command completes. To fork the command into a background process so that !FlexGet continues processing without delay, you not only have to add an ampersand (&) at the end of the command, you have to use the {{allow_background}} option. Note, this option will also prevent !FlexGet from determining if the command failed, so it will not retry. A usage example:
{{{
exec:
  allow_background: yes
  auto_escape: yes
  on_output:
    for_accepted: get_flash_videos %(url)s &
}}}

=== Footnotes ===

 1. Prior to r1552 advanced configuration was it's own plugin, adv_exec.
 2. Prior to r1888 ''phase'' was called ''event''