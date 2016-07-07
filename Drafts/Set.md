# Set 2.0
```
set:
  [FIELD_NAME](/FIELD_NAME): <string format>

  [FIELD_NAME](/FIELD_NAME):
    {value]: <string format>
    [regexp](/regexp): <regexp groups>
    [replace](/replace): [<regexp what>, <with text>]
```

**Simple example:**

```
set:
  path: /foo/bar/%(series_name)s/
```


**Advanced example:**

```
set:
  path:
    value: /foo/bar/%(series_name)s/
    replace: [' ', '.']
```