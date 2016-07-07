# Handling series neatly
While setup described in in the [installation](/Install) is a good start. In practice utilizing it without any further refining leads to some inconveniences. Ie. what if you want to grab series from 4 different feeds?

```
feeds:
  feed_A:
    rss: http://example.com/foo.rss
    series:
      - chuck
      - south park
      .
      .
    download: ~/downloads/series/

  feed_B:
    rss: http://source.com/bar.rss
    series:
      - chuck
      - south park
      .
      .
    download: ~/downloads/series/

  feed_C:
    .
    .

  feed_D:
    .
    .
```

As you can see this gets quite messy, adding new feeds and maintaining series list requires too much work. Which is exactly the thing we are trying to avoid here.

Solution, use [preset](/ModulePreset) plugin!

## Series with preset
```
series:   # this is name of the preset
  series: # this is a plugin in the preset
    - chuck
    - south park
    .
    .
  download: ~/downloads/series/

feeds:
  feed_A:
    rss: http://example.com/foo.rss
    preset: series

  feed_B:
    rss: http://source.com/bar.rss
    preset: series

  .
  .
```

Now your series list is maintained at one place and adding new series feeds is easy and painless!