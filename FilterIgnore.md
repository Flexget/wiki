
<h1 style="color: red">To be removed</h1>


See module [regexp](/FilterRegexp)

# Ignore
Entries matching regexp will be rejected.
Non matching entries are not intervened.
        
This is usefull for rejecting entries containing certain patterns
globally by using global section.

Example:

```
global:
  ignore:
    - pattern 1

feeds:
  feed A:
    patterns:
      - pattern 2
  feed B:
    patterns:
      - pattern 3
```

Entries containing pattern 1 are not downloaded even if they also
match to patterns 2, 3 or pass any other feed filters.

Supports same syntax as [patterns](/FilterPatterns).