= Transfer torrents in transmission to deluge =
{{{Note:}}} This has not been tested, if somebody tests it, please report results and fix the recipe with needed updates.

{{{
tasks:
  migrate_transmission:
    manual: yes  # This means the task only runs when you do `flexget --task migrate_transmission`
    from_transmission: yes  # You may need to specify the connection options to your transmission daemon instead of 'yes'
    set:
      path: "{{transmission_downloadDir}}"  # Make sure deluge saves to same path as transmission
    seen: local
    accept_all: yes
    deluge: yes  # You may need your deluge daemon connection info here