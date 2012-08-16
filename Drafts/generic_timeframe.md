Ideas for a generic timeframe plugin, decoupled from series plugin.

Entries would need to be tagged with a unique content id field to work with this. For example, series plugin might add content_id field set to seriesname.seriesid, and movie content id might be imdb id.

It would also be nice to be able to use any filter plugin to define 'target' criteria. Example config:
{{{
timeframe:
- target:
    quality: 720p
  wait: 6 hours
}}}
This would allow other possibilities like:
{{{
timeframe:
- target:
    regexp:
      reject:
      - fastsub
  wait: 1 day
}}}
'target' is a bit awkward wording in this situation though...

Behind the scenes, timeframe plugin would record the first time an accepted item comes through the feed with a given content_id. Before 'wait' time had expired, it would let the 'target' filter plugin do its rejection on those items. (and store them to backlog if rejected) After 'wait' time expires, it would simply stop running the 'target' filter plugin.

You could even set up multiple level timeframe with this system:
{{{
timeframe:
- target:
    quality: 1080p
  wait: 1 day
- target:
    quality: 720p+
  wait: 2 days
}}}
Meaning, only accept 1080ps on the first day, accept 720ps on the second day, and anything after that.