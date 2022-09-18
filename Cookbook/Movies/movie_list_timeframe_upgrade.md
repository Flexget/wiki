---
title: movie_list_timeframe_upgrade
description: 
published: true
date: 2022-09-18T05:20:16.120Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:20:13.430Z
---

# Fancy Movie List Magic
Series plugin has some really nice features, like timeframe and upgrade, which it might be desirable to replicate with movies. This config shows how you can use multiple tasks to emulate series plugin features like timeframe with upgrade on a list of movies you want.

```
# Since we are making more than one task, which will share some common plugins, let's put some of those plugins in templates.
# Ain't nobody got time to type this crap twice.
templates:
  # Let's put an input plugin (or more than one!) in this template which produces movie releases.
  movie releases to consider:
    # It's a pretty good tracker, maybe Sean will give you that invite to the good stuff he promised you one day.
    rss: http://mytracker.com/newmoviereleases.rss

    # But what if you want to get an old movie? Do you really think that the bluray remaster of 
    # Groundhog Day is just going to magically scroll across your rss right after you add it to your list?
    # We'd better add an input plugin that searches for releases of our wanted movies. (that's the discover plugin)
    discover:
      what:
        # We're gonna use these same plugins again in other places. If you trade out in one place (e.g. trakt_list instead of movie_list,)
        # remember to trade out in the other! (You might want to use YAML's anchor/alias feature to repeat these bits. Someone should write a recipe about that.
        # The important part is that we are keeping track of 2 different lists of movies with list plugins, henceforth known as 'getlist' and 'upgradelist'
        # We want to search for movies on either of these lists
        - movie_list: getlist
        - movie_list: upgradelist
      from:
        # Hurry up already Sean!
        - kat:
            category: movies
            verified: yes


  # Put filters in this template that reject movies you never want, under any circumstances
  never get movies i wont abide:
    quality: 720p+ !cam
    regexp:
      reject:
        - really.crappy.release.group


  # I guess we could have used one template instead of 3 different ones. After all, we are using all our
  # templates on both of our tasks. But 'movie input and some filters and also the output plugin, but nothing that accepts anything'
  # just feels like a really long and cumbersome template name, doesn't it? I think we made a good decision.
  this is how I download things:
    # Maybe instead of deluge plugin you want transmission plugin, or something else.
    deluge:
      path: /mnt/thegooddrive/movies/


# Alright, we've got some templates. But those don't do anything, let's use them in a couple tasks to get things done.
tasks:
  # These are the movies you want because they are available now, but want to upgrade later
  get movie standins:
    template:
      - movies to consider
      # Screw these movies, maybe your little cousin finds the quality to be okay, but not you. You'd rather eat dirt.
      # Coincidentally, something that Will (that's the cousin's name, isn't it?) also likes doing.
      - never get movies i wont abide
      - this is how i download things
       
    # If you want to wait a bit after seeing releases in this category before accepting them
    # (Maybe the good release will be out in a couple of hours! You don't want to waste your time on this one if that's the case.)
    delay: 12 hours  # We'll wait 12 hours for the keepers task to maybe accept a movie before we accept one here
    list_match:
      from:
        # You could use a different list plugin that supports movies here if you want, like trakt_list, or imdb_list
        # 'getlist' is our main list of movies we are waiting to download, it might be easier to use one of the online
        # plugins here, so you can add movies to your list from a website/app like trakt/imdb.
        - movie_list: getlist
    # Well, we're getting the 720p version. But that's not good enough for the permanent collection is it?
    # list_match will automatically remove this movie from our 'getlist' when a release is accepted, but
    # let's remember to add this movie on our 'upgradelist', to make sure we get a good copy later.
    list_add:
      # This could also be a different list plugin than movie_list
      - movie_list: upgradelist


  # These are the ones you want, even if you've gotten stand ins before
  get movie keepers:
    # Good thing we made concise templates with good names, so we don't have to type a lot of the same stuff in multiple tasks.
    template:
      - movies to consider
      - never get movies i wont abide
      - this is how i download things
    # We ain't accepting nothing but the best in this task, let's add some filters to keep out the undesirables.
    # That snob Katie won't have anything snarky to say next time.
    quality: 1080p+ bluray+
    # We'll accept any movies from either of our lists in this task.
    list_match:
      from:
        - movie_list: getlist
        - movie_list: upgradelist


# Alright, I'm pretty sure we got daemon mode running right? Let's schedule our tasks to run periodically.
schedules:
  # Let's make sure we always run the keepers task first, hope springs eternal.
  - tasks: [get movie keepers, get movie standins]
    interval:
      # Let's be real, you should be going to bed anyway. Running this more often is only going to
      # clog the tubes. (Of the internet. (Think of the starving children who need those tubes. (You monster.)))
      hours: 6
```

## Things that would have been linked
Who decided to write everything in comments in a code block? You can't even put links in there!
Here are some things that would have been linked above, had that happened.

### Input Template
Other input plugins can be found [here](/Plugins#Inputs). You can add to, remove or replace any of the ones in the `movie releases to consider` template of this recipe with others.
Remember that you want input plugins that produce actual download links for movies in here.

### Output Template
Other output plugins are [here](/Plugins#Output). This recipe is assuming you are dealing with torrents, make the appropriate adjustments to both input and output plugins if not.

### Movie Lists
We used a list plugin to represent 2 lists in this recipe. In our this case, it was the `movie_list` plugin, where we defined 2 named lists, that we used in multiple contexts. You can switch out `movie_list` for any of the list plugins [here](/Plugins/List), (pick one that supports movies though,) just remember to change all instances of the 'getlist' or 'upgradelist' list at the same time.

### YAML !Anchor/Alias
Nobody wrote a cookbook entry about anchor/alias. But somebody did write about it on the forum, you can read about it [here](http://discuss.flexget.com/t/advanced-yaml-trick-anchors/2405?u=gazpachoking). This can be useful for repeating the same bit of config in different contexts, for example repeating the same list plugin config in `list_match`, `list_add`, and `discover`.