## Regexp
## !! This is for for old 0.9 version !!
Please see [plugins](/Plugins) page for current version.

Use regular expression to Accept, Filter or Reject entries. FlexGet uses python regexp format and all matching is done case insensitive. This module may look a bit scary but in reality you rarely want anything more than what simple examples describe.

### Simple examples
Accept entries matching regexp(s) and filter rest of the entries.

```
regexp:
  accept:
    - pattern
  rest: filter
```

Filter entries matching regexp(s), they can still be accepted by other modules. This should be used when you want to leave chance of accepting to other modules.

```
regexp:
  filter:
    - pattern
```

Reject permanently entries matching regexp(s). This should be used when you absolutely do not want to download matching entries, even if some other module (ie. FilterImdb) would deem them acceptable.

```
regexp:
  reject:
    - pattern
```

Multiple operations. This would be useful when grabbing some shows and they appear with unwanted languages as well.

```
regexp:
  accept:
    - show name
  reject:
    - german
    - sweden
  rest: filter
```

## Set custom path
Any regexp rule can set custom path for matching entry.

### Example
```
regexp:
  accept: 
    - pattern: ~/custom/path
  rest: filter
```

or

```
regexp:
  accept: 
    - pattern:
        path: ~/custom/path
  rest: filter
```

## Full syntax
```
regexp:
  <operation>:
    - pattern 1
    - pattern 2: <custom path>
    - pattern 3:
        [not](/not):
          - pattern 4
        [path](/path): <custom path>
  [rest](/rest): <operation>
```

Available operations: `accept`, `filter`, `reject`, `accept_excluding`, `filter_excluding` and `reject_excluding`.
Rest and not parameters are optional. Configuration may contain any number and combination of different operations.