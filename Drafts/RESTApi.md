= '''REST API ''' =

== Design Guidelines ==

- All data should be transferred as JSON.
- Stick to REST principles as long as it makes sense.

= Endpoints =

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