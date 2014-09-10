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

== Core Endpoints ==

=== /execute ===
Calling this would cause an execution to occur. Should options for the execution can be specified as urlencoded parameters, or json post data? I'm thinking both will be allowed.
What should the return value be? Should we be able to request logs of this execution? Maybe return value is an execution id that can be passed to a log endpoint.