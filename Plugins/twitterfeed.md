# twitterfeed
Creates [entries](/Entry) from a twitter account by looking at urls in tweets. This is most likely to be used with the [eztv](https://twitter.com/eztv_it) twitter account.

### Example
```
twitterfeed:
  account: <account>
  consumer_key: <consumer_key>
  consumer_secret: <consumer_secret>
  access_token_key: <access_token_key>
  access_token_secret: <access_token_secret>
```

By default, the 50 last tweets are fetched corresponding to the option:
```
all_entries: yes
```

To change that default number:
```
tweets: 75
```

Beware that Twitter only allows 300 requests during a 15 minutes window.

If you want to process only new tweets:
```
all_entries: no
```

That option's behaviour is changed if the corresponding task's
configuration has been changed. In that case, new tweets are
fetched and if there are no more than `tweets`, older ones are
fetched to have `tweets` of them in total.

