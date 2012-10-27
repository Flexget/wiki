= Seed series DB with existing episodes =
Sometimes when you first set up !FlexGet, it is useful to seed the series database with the episodes you already have for your shows. This helps !FlexGet learn what type of series numbering your shows have, as well as what episodes you already have. This can be accomplished by making a special task which you will run after setting up !FlexGet.
{{{
presets:
  presetwithyourseriesconfig:
    # your series config, (or import_series) goes here
    # this preset can then be used for the seed_series_db task, as well as your normal downloading tasks
tasks:
  seed_series_db:
    # The find plugin will find all of your existing episodes
    find:
      regexp: .*(avi|mkv|mp4)$
      path: /my/series
      recursive: yes
    preset: presetwithyourseriesconfig
    # We use the manual plugin so that this task only runs when explicitly called
    manual: yes
}}}
Now, you can run {{{flexget --task seed_series_db --disable-advancement}}} to run this task and let the series plugin learn about your existing episodes. This should only need to be done when you first set up !FlexGet, or when you add a new show to your config which you already have episodes downloaded for.

You can test to see if it worked by running a [wiki:Plugins/series#a--series --series] report.

'''NOTE:''' Be careful if you are using a global preset. We do not want any output plugins (or any other plugins) to be run on this task.