= Digest =
This plugin works as an output plugin, and collects entries from tasks to be combined into another task (usually for notification.) It is used with `emit_digest` plugin in the task where the entries should be collected.

== Examples ==
These examples are incomplete, and contain comments where other plugins should be set up.
=== Daily Email ===
{{{
tasks:
  download task 1:
    # some stuff to do downloads
    digest: daily email
  download task 2:
    # some stuff to do downloads
    digest: daily email
  daily email task:
    emit_digest:
      list: daily email
    seen: local
    email:
      # the email settings
schedules:
- tasks: [download task 1, download task 2]
  interval: 1 hour
- tasks: daily email task
  interval: 1 day
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
    seen: no
    make_html:
      # the make_html settings
schedules:
- tasks: [download task 1, download task 2, generate html]
  interval: 1 hour
}}}