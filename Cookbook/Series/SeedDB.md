# Seed series DB with existing episodes
### Note:
This is only necessary when using discover and you want to continue getting new episodes from whatever you have at disk. 


### Recipe
This helps FlexGet learn what type of series numbering your shows have, as well as what episodes you already have. This can be accomplished by making a special task which you will run after setting up FlexGet.

```yaml
templates:
  tv:
    # Your series config

tasks:
  seed-series-db:
    # Only run when explicitly called
    manual: yes
    # Find all of your existing episodes
    filesystem:
      regexp: .*(avi|mkv|mp4)$
      path: /my/series
      recursive: yes
    template: tv
```

Now, you can run `flexget execute --tasks seed-series-db --disable-advancement --learn` to run this task and let the series plugin learn about your existing episodes. This should only need to be done when you first set up FlexGet, or when you add a new show to your config which you already have episodes downloaded for.

You can test to see if it worked by using the [series plugin command line interface](/Plugins/series#seriesCommandlineArguments).

**NOTE:** Be careful if you are using a global template. We do not want any output plugins (or any other plugins) to be run on this task.