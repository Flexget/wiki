= NPO watchlist =

Produces entries for every episode on the user's npo.nl watchlist (Dutch public television). To add series / episodes, login to [[http://www.npo.nl | npo.nl]] and add them to your profile.

Entries can be downloaded using [[https://bitbucket.org/Carpetsmoker/download-npo | download-npo]].

||='''Option'''=||='''Description'''=||
||'''email'''||Your username for npo.nl||
||'''password'''||Your password for npo.nl||
||'''remove_accepted'''||If set to 'yes', the plugin will delete accepted entries from the watchlist after download is complete. Defaults to 'no'.||

== Example ==

{{{
your_task:            
  npo_watchlist:
    email: aaaa@bbb.nl
    password: xxx
    remove_accepted: yes
  accept_all: yes
  exec:
    fail_entries: yes
    auto_escape: yes
    on_output: 
      for_accepted:
        - download-npo -o "path/to/directory/{{series_name_plain}}" -f "{serie_titel} - {datum} {aflevering_titel} ({episode_id})" -t {{url}}
}}}