# Download NBA games from RuTracker.org

One could easily download all kinds of stuff from [RuTracker](https://rutracker.org), it doesn't even requires authentication to do that, thanks to `rutracker` plugin.

```
variables:
  # RuTracker forum id, look it up in URL
  # e.g. https://rutracker.org/forum/viewforum.php?f=1997
  rtr_f_id: 1997
tasks:
  nba_tracker:
    rss:
      url: "http://feed.rutracker.cc/atom/f/{? rtr_f_id ?}.atom"
      other_fields:
        # we'll use this feed entry attribute to filter only recent entries
        - updated
    regexp:
      accept:
        # you could filter entries by your team's name, at least NBA section
        # has pretty rigid title format rules
        - "Golden State Warriors"
        # WA-A-ARRIORS! =)
        # remove this "match-all" regexp to enable filtering by team
        - "."
      reject:
        # screw commentary in Russian
        - RU
    age:
      # usually you want the latest games, right?
      age: 1 days
      field: updated
      action: reject
    # if you don't set quality, you are likely to download two or three files
    # for each game
    quality: 1080p
    # and now for some magic!
    manipulate:
      - updated:
          extract: '^([^+]+)'
      - teams_n_date:
          from: title
          extract: '([0-9.]{8,10} / \{[A-Za-z0-9 @]+\})'
    unique:
      field: teams_n_date
```