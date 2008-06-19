= Daemon / Scheduler =

Implement daemon mode + scheduler.

Configuration draft:

{{{
schedule:
  feed_name:
    # TODO
  another_feed:
    # TODO
}}}

Note, it should be possible to define interval as minutes, hours, days and ideally all these either per day or every day.

Daemon / schedule mode trough --daemon parameter (status | start | stop | reload).