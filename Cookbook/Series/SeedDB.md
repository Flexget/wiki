# Seed series DB with existing episodes

## Note

This is rather complicated and mostly useless as series plugin will continue from next episode it sees in the feed. Some times it may get stuck to wrong older episode for example if S01E01 happens to appear as first episode FlexGet sees but the series is already going on second season. Even then you can tell FlexGet to ignore that and continue from later episodes but this may be a problematic if you have hundreds of shows. This recipe may come in handy then.


## Recipe

This helps FlexGet learn what type of series numbering your shows have, as well as what episodes you already have. This can be accomplished by making a special task which you will run after setting up FlexGet.

```
templates:
  tv:
    # your series config, (or import_series) goes here
    # this template can then be used for the seed_series_db task, as well as your normal downloading tasks
tasks:
  seed_series_db:
    # The filesystem plugin will find all of your existing episodes
    filesystem:
      regexp: .*(avi|mkv|mp4)$
      path: /my/series
      recursive: yes
      retrieve: files
    template: tv
    # We use the manual plugin so that this task only runs when explicitly called
    manual: yes
```

Now, you can run `flexget --task seed_series_db --disable-advancement --learn` to run this task and let the series plugin learn about your existing episodes. This should only need to be done when you first set up FlexGet, or when you add a new show to your config which you already have episodes downloaded for.

You can test to see if it worked by running a [`flexget series list`](/CLI/series) report.

*NOTE:* Be careful if you are using a global template. We do not want any output plugins (or any other plugins) to be run on this task.