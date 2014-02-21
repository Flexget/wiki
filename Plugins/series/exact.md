== Exact mode ==

Enable strict name matching. Useful for differentiating between series whose names start similarly.

'''Example'''

{{{
series:
  - Test:
      exact: yes
  - ABC
  - ABC LA
}}}

Enabling `exact` changes the mechanism so that the series name must be immediately followed by the episode number. With previous example ie. `Test Bar S01E01` would not be considered valid `Test`.

Series plugin will also auto enable exact matching if it detects that there are series configured which need it in order not to be confused with each others. In the example series `ABC` would auto-enable exact matching since that name can be confused to `ABC LA`.

'''Forget...'''[[BR]]
In case you have situation where !FlexGet is downloading episodes from another series with similar name, turn on the `exact` manually. You may also need to reset the series status with `series forget NAME` in case wrong episodes have been downloaded and it confuses ''episode advancement''.
Forgetting single episode is also possible by `series forget "NAME" sxxexx`, where xx is season number and episode number. In case you want to add some already watched episode have a look at [wiki:Plugins/series/begin series begin].
