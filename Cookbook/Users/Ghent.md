---
title: Ghent
description: 
published: true
date: 2022-09-18T05:22:35.347Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:22:32.799Z
---

This is my configuration.  I try to keep things as simple as possible.  I lean heavily towards scene releases as they're confirmed clean and have good quality.

Because I pull from a site that uses unrarred files and you subscribe to shows along with another site that is more vanilla I have 2 templates that are anchored to each other using the power of YAML.

Updated: 2016-07-07

```
# vim: tabstop=2 softtabstop=2 expandtab:

secrets: secrets.yml

schedules:
#  - tasks: seed-series-db
#    interval:
#      hours: 4
  - tasks: extract-rars
    interval:
      minutes: 15
  - tasks: [trakt-new, ipt-tv-rss, stv-tv-rss]
    interval:
      minutes: 15
  - tasks: trakt-clean
    interval:
      hours: 4

templates:
  # template: shows-custom
  shows-custom:
    series:
      custom:
        - Black Sails:
            upgrade: yes
            qualities:
              - 720p|1080p
        - Chicago P.D.:
            alternate_name:
              - Chicago PD
        - The Expanse:
            upgrade: yes
            qualities:
              - 720p|1080p
        - The Flash:
            alternate_name:
              - The Flash 2014
        - Game of Thrones:
            upgrade: yes
            qualities:
              - 720p|1080p
        - Kingdom 2014:
            alternate_name:
              - Kingdom
            exact: yes
        - The Magicians US:
            alternate_name:
              - The Magicians
        - Outsiders:
            alternate_name:
              - Outsiders 2016
            exact: yes
        - Rizzoli & Isles:
            alternate_name:
              - Rizzoli and Isles
        - Shameless US:
            alternate_name:
              - Shameless
            upgrade: yes
            qualities:
              - 720p|1080p
        - The Shannara Chronicles:
            upgrade: yes
            qualities:
              - 720p|1080p
        - Teachers:
            alternate_name:
              - Teachers 2016
            exact: yes
        - Vikings:
            upgrade: yes
            qualities:
              - 720p|1080p
            upgrade: yes
        - The Voice:
            exact: yes
        - Young & Hungry:
            alternate_name:
              - Young and Hungry

  # template: no-groups
  no-groups:
    series:
      settings:
        custom: &anc-tv-default
          identified_by: ep
          quality: 720p
          propers: yes

  # template: rls-groups
  rls-groups:
    series:
      settings:
        custom: &anc-rls-groups
          <<: *anc-tv-default
          from_group:
            - 0SEC
            - 2HD
            - AVS
            - ALTEREGO
            - BATV
            - BRISK
            - CROOKS
            - CTU
            - CURIOSITY
            - DHD
            - DIMENSION
            - EVOLVE
            - FAILED
            - FIHTV
            - FLEET
            - FOV
            - IMMERSE
            - KILLERS
            - LEGI0N
            - M33P
            - ORENJI
            - PSYPHER
            - TASTETV
            - TLA
            - W4F


tasks:
  # task: seed-series-db
  seed-series-db:
    manual: yes
    template: [shows-custom, no-groups]
    disable: seen
    filesystem:
      path: /var/data/ghent/media/tvshows
      mask: '*.mkv'
      recursive: yes
      retrieve:
        - files
        - symlinks
    configure_series:
      settings: *anc-tv-default
      from:
        trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: Plex Shows
          type: shows
          strip_dates: yes

  # task: trakt-new
  trakt-new:
    disable: seen
    trakt_list:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
      list: Plex Add
      type: episodes
      strip_dates: yes
    accept_all: yes
    set_series_begin: yes
    list_add:
      - trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: Plex Shows
          type: shows
    list_remove:
      - trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: Plex Add

  # task: trakt-clean
  trakt-clean:
    disable: seen
    trakt_list:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
      list: Plex Shows
      type: shows
    trakt_lookup:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
    if:
      - trakt_series_status == 'canceled' or trakt_series_status == 'ended': accept
    list_remove:
      - trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: Plex Shows
    list_add:
      - trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: Plex Removed
          type: shows

  # task: ipt-tv-rss
  ipt-tv-rss:
    template: [shows-custom, rls-groups]
    rss: '{{ secrets.rss.ipt }}'
    exists_series:
      - /var/data/ghent/media/tvshows
    configure_series:
      settings:
        <<: *anc-rls-groups
        exact: yes
      from:
        trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: Plex Shows
          type: shows
          strip_dates: yes

    content_filter:
      require:
        - '*.rar'
    download: /home/ghent/var/dropbox/torrent/auto/seed

  # task: stv-tv-rss
  stv-tv-rss:
    template: [shows-custom, no-groups]
    rss: '{{ secrets.rss.stv }}'
    exists_series:
      - /var/data/ghent/media/tvshows
    download: /home/ghent/var/dropbox/torrent/auto/tvshows
    configure_series:
      settings: *anc-tv-default
      from:
        trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: Plex Shows
          type: shows
          strip_dates: yes
    download: /home/ghent/var/dropbox/torrent/auto/tvshows

  # task: extract-rars
  extract-rars:
    manual: yes
    inputs:
      - filesystem:
          path: /var/data/ghent/torrent/seed
          mask: '*.rar'
          recursive: yes

    # Looks and accepts the first rar file of every archive set
    regexp:
      accept_excluding:
        - part([0-9]{2,4}|[2-9]).rar$
      accept:
        - part01.rar$
        - part001.rar$
      # Find plugin doesn't put the extension in the titles of
      # entries, so we need to tell it to look at the location
      from: location

    # Disregard already processed files
    only_new: yes

    # Send files to winrar to be unpacked, winrar must be installed to default path
    exec:
      allow_background: no
      auto_escape: no
      fail_entries: yes
      on_output:
        for_accepted: >
          /opt/bin/unrar e -o- -idq "{{location}}" "/var/data/ghent/process/unrarred"
```