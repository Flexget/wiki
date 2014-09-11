= '''REST API ''' =

Anyone interested in developing the webui should feel free to input here.

== Design Guidelines ==

- All data should be transferred as JSON.
- Stick to REST principles as long as it makes sense.
- Should be some easy way for plugins to add their own api endpoints.

= Core Endpoints =

== Execution ==
Executions would be represented with a data structure something like this.
`{"id": "some id for execution", "status": "running|pending|complete|aborted"}`

==== /execution ====

'''GET'''
Return a list of running/pending executions.

'''POST'''
Adds an execution to the queue. Accepts options as JSON (maybe also url parameters).
Returns execution info.

=== /execution/<id> ===

'''GET'''
Get status of execution with given id.

=== /execution/<id>/log ===
'''GET''' Streams the log for execution with given id.

== Configuration ==
Not quite sure how this one should go yet. I'm thinking core only provides a way to edit root level config keys (tasks, schedules, etc.) and if we need more granular editing, the plugin would be responsible for the endpoints (e.g. editing individual schedules would be handled by scheduler plugin)

= Plugin Endpoints =

== movie_queue ==
id for movie will be primary key from our database. Not online provider id.
=== /movie_queue ===
'''GET''' Return list of movies in the queue

'''POST''' Add a movie to the queue.
=== /movie_queue/<id> ===
'''GET''' Return details for movie in queue (not metainfo from imdb etc.)

'''DELETE''' Remove movie from queue.

'''PUT''' Change details for movie in queue
== series ==
== history ==
=== /history ===
'''GET''' Get list of items in history
