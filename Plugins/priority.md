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