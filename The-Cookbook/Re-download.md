= How to re-download already downloaded items =

{{{
rss: ....
regexp:
  accept:
    - <pattern>: { set: { immortal: yes } }
download: ....
}}}

This will force !FlexGet to download items matching <pattern> on every execution.