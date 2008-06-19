= Daemon / Scheduler =

Implement daemon mode + scheduler.

'''Configuration draft''':

{{{
schedule:
  default:
    .
    .
  feed_name:
    .
    .
  another_feed:
    .
    .
}}}

Note, it should be possible to define interval as minutes, hours, days and ideally all these either per day or every day.

'''Draft 1:'''

{{{
schedule:
  default:
    *: 1 hours      # default interval for all days (* may not be valid key?)
  some_feed:
    tue: 10 minutes # overrides tuesday from default
    wed: None       # no scheduling for wednesday
}}}

Daemon / schedule mode trough --daemon parameter (status | start | stop | reload).