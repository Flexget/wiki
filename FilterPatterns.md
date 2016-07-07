
<h1 style="color: red">To be removed in 1.0</h1>


See module [regexp](/FilterRegexp)

# Patterns
[Entries](/Entry) matching any of the given regular expression are accepted. Non-matching entries are filtered.

### Example
```
patterns:
  - regular expression
  - another regular expression
```

**Notes:** Regular expression is tested from [Entry](/Entry) title **and** url. Regular expression is case-insensitive.

## Advanced users:
It's also possible to specify custom download path for
pattern and secondary regexp(s) that causes entry to be
filtered even when primary regexp matches entry.

Examples:

```
patterns:
  # simplest way to specify custom path
  - regexp1: ~/custom_path/

  # alternative way to specify custom path
  - regexp2:
      path: ~/custom_path/

  # specify custom path and secondary single filter regexp
  - regexp2:
      path: ~/custom_path/
      not: regexp3

  # multiple secondary filter regexps
  - regexp4:
      not:
        - regexp5
        - regexp6

  # Tip: In yaml you can write dictionaries and lists in inline form.
  # Above examples can be also written as:
  - regexp2: {path: ~/custom_path/, not: regexp3}
  - regexp4: {not: [regexp5, regexp6]}
```