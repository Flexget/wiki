= Digest =
This plugin works as an output plugin, and collects entries from tasks to be combined into another task (usually for notification.) It is used with `emit_digest` plugin in the task where the entries should be collected.

== Configuration ==
{{{
digest: <listname>
}}}
or
{{{
digest:
  list: <listname>
  state: [accepted|rejected|failed|undecided]
}}}
You can also specify a list of states to be digested.
{{{
digest:
  list: <listname>
  state:
    - accepted
    - failed
}}}

== Examples ==
These examples are incomplete, and contain comments where other plugins should be set up.
=== Daily Email ===
{{{
tasks:
  download task 1:
    # some stuff to do downloads
    digest:
      list: daily email
      state:
        - accepted
        - failed

  download task 2:
    # some stuff to do downloads
    digest: daily email

  daily email task:
    emit_digest:
      list: daily email
      restore_state: yes
    seen: no
    email:
      # the email settings

schedules:
- tasks: [download task 1, download task 2]
# interval:
#  <weeks|days|hours|minutes>: <#>
  interval:
    hours: 1
- tasks: daily email task
  interval:
    days: 1
}}}

=== Last 50 entries HTML ===

{{{
tasks:
  download task 1:
    # some stuff to do downloads
    digest: recently accepted

  download task 2:
    # some stuff to do downloads
    digest: recently accepted

  generate html:
    emit_digest:
      list: recently accepted
      limit: 50
      expire: no
    accept_all: yes
    seen: no
    make_html:
      # the make_html settings

schedules:
- tasks: [download task 1, download task 2, generate html]
  interval:
    hours: 1
}}}