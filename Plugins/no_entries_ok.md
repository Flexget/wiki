= No Entries Ok =

!FlexGet normally expects a task to produce entries on every run, and outputs a warning if no entries were produced:
{{{
Task didn't produce any entries. This is likely due to a mis-configured or non-functional input.
}}}
If you have a task where this is not indicative of a problem, you can silence this warning, by including this plugin in the task.
=== Configuration ===
{{{
no_entries_ok: yes
}}}