I use the premiere plugin to download new shows. However it seems it is broken as it not only downloads EP 00 and 01 but also more.

Config excerpt:

```
templates:
  global:
    cookies: ~/.flexget/cookies.sqlite
    regexp:
      reject:
        - xxx

  tv_common:
    inputs:
      - rss: xxx
      - rss: yyy
    verify_ssl_certificates: no
    download: ~/rtorrent/Watch/
    exists_series:
      - xxx

tasks:
  premiers_lq:
    template: tv_common
    series_premiere:
      propers: no
      allow_seasonless: yes
    content_size:
      max: 500
      strict: no
    thetvdb_lookup: yes
    require_field: tvdb_genres
    regexp:
      reject:
        - xxx

schedules:
  - tasks: [premiers_lq]
    interval:
      minutes: 20
```

```
flexget series show "Battle Girl High School"
There is a FlexGet process already running for this config, sending execution there.

┌Battle Girl High School Battle Girl Project────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┬──────────────────┬────────┐
│ Identifier │ Last seen │ Release titles                                                                                                                                                                                               │ Release Quality  │ Proper │
├────────────┼───────────┼──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼──────────────────┼────────┤
│ S01E01     │ 6h        │ Battle Girl High School: Battle Girl Project - S01E01 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Battle Girl High School - 01 [1080p] ] * │ 1080p webdl h264 │        │
│ S01E03     │ 1h        │ Battle Girl High School: Battle Girl Project - S01E03 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Battle Girl High School - 03 [1080p] ] * │ 1080p webdl h264 │        │
│ S01E04     │ 1h        │ Battle Girl High School: Battle Girl Project - S01E04 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Battle Girl High School - 04 [1080p] ] * │ 1080p webdl h264 │        │
│ S01E02     │ 1h        │ Battle Girl High School: Battle Girl Project - S01E02 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Battle Girl High School - 02 [1080p] ] * │ 1080p webdl h264 │        │
│ S01E05     │ 1h        │ Battle Girl High School: Battle Girl Project - S01E05 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Battle Girl High School - 05 [1080p] ] * │ 1080p webdl h264 │        │
└────────────┴───────────┴──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┴──────────────────┴────────┘
 * Downloaded

 `Battle Girl High School Battle Girl Project` uses `ep` mode to identify episode numbering.
 See `identified_by` option for more information.
 ```
 
 ```
 grep -i "battle girl" flexget.log
2017-08-02 09:32 INFO     download      premiers_lq     Downloading: Battle Girl High School: Battle Girl Project - S01E01 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Battle Girl High School - 01 [1080p] ]
2017-08-02 14:52 INFO     download      premiers_lq     Downloading: Battle Girl High School: Battle Girl Project - S01E03 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Battle Girl High School - 03 [1080p] ]
2017-08-02 14:52 INFO     download      premiers_lq     Downloading: Battle Girl High School: Battle Girl Project - S01E04 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Battle Girl High School - 04 [1080p] ]
2017-08-02 14:52 INFO     download      premiers_lq     Downloading: Battle Girl High School: Battle Girl Project - S01E02 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Battle Girl High School - 02 [1080p] ]
2017-08-02 14:52 INFO     download      premiers_lq     Downloading: Battle Girl High School: Battle Girl Project - S01E05 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Battle Girl High School - 05 [1080p] ]
```

It hasn't been the only show but there have been many others, e.g. also today:

```
grep -i "action heroine" flexget.log
2017-08-02 09:52 INFO     download      premiers_lq     Downloading: Action Heroine Cheer Fruits - S01E01 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Action Heroine Cheer Fruits - 01 [1080p] ]
2017-08-02 14:52 INFO     download      premiers_lq     Downloading: Action Heroine Cheer Fruits - S01E04 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Action Heroine Cheer Fruits - 04 [1080p] ]
2017-08-02 14:52 INFO     download      premiers_lq     Downloading: Action Heroine Cheer Fruits - S01E03 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Action Heroine Cheer Fruits - 03 [1080p] ]
2017-08-02 14:52 INFO     download      premiers_lq     Downloading: Action Heroine Cheer Fruits - S01E02 [ 2017 ] [ MKV | H.264 | WEB-DL | 1080p | FastTorrent | Foreign ] [ Uploader: lhdlovebooh ]  [ [HorribleSubs] Action Heroine Cheer Fruits - 02 [1080p] ]
```

As you can see, it was all downlaoded with the premiers_lq taks which should only download premiere episodes.
