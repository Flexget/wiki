= Priority =

Change feed execution order, without explicitly setting priority feeds are executed in more or less random order. Execution order is 1,2,3...

'''Example'''

{{{
feeds:
  feed a:
    priority: 10
  feed b:
    priority: 20
  feed c: 
    priority: 5
}}}

In this example order is ''feed c, feed a, feed b''.

You don't need to give priority to all feeds in your config. Just up the ones you wish to execute first. You can even put multiple feeds with same priority number, in which case they will be executed with same priority but order is random within that priority.

