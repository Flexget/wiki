---
title: twitterfeed
description: 
published: true
date: 2022-09-18T05:15:47.434Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:15:44.818Z
---

# twitterfeed
Creates [entries](/Entry) from a twitter account by looking at urls in tweets. 

### Example
```text
twitterfeed:
  account: <account>
  consumer_key: <consumer_key>
  consumer_secret: <consumer_secret>
  access_token_key: <access_token_key>
  access_token_secret: <access_token_secret>
```

| Option | Description |
| ---|---|
| all_entries | By default, the 50 last tweets are fetched corresponding to the option. <br>Set to `yes` to fetch everything. If you want to process only new tweets set to `no`. <br>Behaviour is changed if the corresponding task configuration has been changed. In that case, new tweets are fetched and if there are no more than `tweets`, older ones are fetched to have `tweets` of them in total. |
| tweets | Change that default number| 

Beware that Twitter only allows 300 requests during a 15 minutes window.
