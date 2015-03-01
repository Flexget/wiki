= Transfer torrents in transmission to deluge =

{{{
tasks:
  migrate_deluge:
    manual: yes # do not run this task automatically - only with flexget execute --tasks migrate_deluge
    from_deluge:
        config_path: "/home/username/.config/deluge" # you need to change path to another one - check your deluge config
    set:
      path: "{{deluge_path}}" # to be sure that transmission downloads to the same path as deluge
    seen: local
    accept_all: yes
    deluge: no
    transmission: yes # you may need to setup connection info here
    disable:
      - seen
      - seen_info_hash
}}}