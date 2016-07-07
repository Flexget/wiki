# Some memos for future
This page is used as internal memo :)

## New configurator / validator
```
>>> v = Validator('dict')
>>> v.accept('key_name', 'text') 
>>> l = v.accept('another_key', 'list')
>>> l.accept('text')
>>> d = l.accept('dict')
>>> d.accept('key', 'number')

Validate:

>>> config = {'key_name': 'foo' .... }
>>> v.validate(config)

Return list of errors in some form.

```

## Add new validators runtime
```
some_base_class?.add_validator('name', Class)
```

## Query configuration from validator
This will be used in future web-ui to generate configuration UI
 
```
>>> d.accepted()
>>> {'key_name':'text', 'another_key':'list'}

>>> l.accepted()
>>> ['text', 'dict']
```