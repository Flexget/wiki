= Daemon / Scheduler =

Implement daemon mode + scheduler.

Configuration draft:

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

Daemon / schedule mode trough --daemon parameter (status | start | stop | reload).