= Age =

Simple plugin to filter based on age. The age is determined via a date set in an entry field. It can for example be used in conjunction with entries created by [wiki:Plugins/filesystem filesystem], which sets the fields `access`, `modified`, `created`, which are last accessed, last modified and file creation respectively.

== Plugin settings ==

Currently the following settings are supported:

{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''field'''||Entry field eg. 'access'||
||'''age'''||The age to be filtered eg. `7 days`. Format: [n] [minutes|hours|days|months]||
||'''action'''||`reject` or `accept` entries||
}}}
== Examples ==
Example task to delete video files that have not been accessed in the last 7 days:

{{{
tasks:
  delete_by_age:
    filesystem:
      path:
        - /some/path
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
      retrieve: files
    age:
      field: 'access'
      action: 'accept'
      age: '7 days'
    exec:
      on_exit:
        for_accepted: rm -f "{{location}}"
}}}