= Some memos for future =

This page is used as internal memo :)

== New configurator / validator ==

{{{
>>> v = Validator('dict')
>>> v.accept('key_name', 'text') 
>>> l = v.accept('another_key', 'list')
>>> l.accept('text')
>>> d = l.accept('dict')
>>> d.accept('key', 'number')

Validate:

>>> v.validate({'key_name': 'foo' .... })

Return list of errors in some form.


Query:

This will be used in future web-ui to generate configuration UI

>>> d.accepted()
>>> {'key_name':'text', 'another_key':'list'}

Query:

>>> l.accepted()
>>> ['text', 'dict']
}}}