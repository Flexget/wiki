== Episode advancement ==

Series plugin keeps track of downloaded episodes for each series and rejects episodes that are too far in the past. Small margin from latest episode is allowed.

'''Example:'''
Series Chuck latest episode is S02E22 and suddenly a feed contains S01E01 which series plugin has not seen or downloaded.[[BR]]
'''Result:'''
Episode advancement rejects this episode since it's too far in the past.

'''Example:'''
Series Chuck latest episode is S02E22 and suddenly a feed contains S02E20 which series plugin has not seen or downloaded.[[BR]]
'''Result:'''
Episode advancement does not reject this. This fits inside grace margin from latest episode.


Advancement can sometimes be problematic if you have huge gap of recent episodes in `--series` database. You can temporarily disable this feature with `--disable-advancement` option allowing !FlexGet to grab latest episode and continue properly from there.
