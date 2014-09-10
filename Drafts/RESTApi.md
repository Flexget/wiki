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