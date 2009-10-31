= Exec = 

Execute command for entries that reach output.

=== Example: ===

{{{
exec: echo "found %(title)s at %(url)s" >> file
}}}

You can use all (available) entry fields in the command.