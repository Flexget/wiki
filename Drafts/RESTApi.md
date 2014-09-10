= '''REST API ''' =

== Design Guidelines ==

Available options:
 * JSON post for large post of information
{{{    
      'action': {
          'oneOf': [
            { 'type': 'object' },
            { 'type': 'boolean'},
            { 'type': 'string' }
           ]
          }
}}}
 * URL encoded posts
{{{
    /{{action}}?{{options}}
}}}

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

