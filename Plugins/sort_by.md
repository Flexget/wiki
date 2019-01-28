# Sort By
Sorts task entries in order by a specified field. Useful for generating RSS in particular order.

### Plugin Options
| Option| Description |
| --- | --- |
| field | The field by which to sort the entries. Default: _title_. **Required** if you are utilizing either of the other two options. |
| reverse | If set to `yes`, reverses the order of the sort. |
| ignore_articles | If set to `yes`, ignores 'a', 'an', and 'the' when sorting. Alternatively, this can be set to a regular expression of articles to be ignored (useful if you primarily use a different language). `yes` is equivelant to using the regex `^(the|a|an)\s`. |

### Example
These entries will be used for the following examples.
```text
His Entry
The Cats Entry
My Entry
```

#### Basic Usage
Config:
```yaml
sort_by: title
```
Result:
```yaml
His Entry
My Entry
The Cats Entry
```

#### Reverse Order of Results
Config:
```yaml
sort_by:
  field: title
  reverse: yes
```
Result:
```yaml
The Cats Entry
My Entry
His Entry
```

#### Ignoring articles
Config:
```yaml
sort_by:
  field: title
  ignore_articles: yes
```
Result:
```yaml
The Cats Entry
His Entry
My Entry
```

#### Ignoring articles with custom regex
Config:
```yaml
sort_by:
  field: title
  ignore_articles: '^(his|my)\s'
```
Result
```yaml
# note that 'His Entry' and 'My Entry' will be considered identical for the sort (since 'His' and 'My' will be ignored) and may be reversed, but will always be before 'The Cats Entry'
My Entry
His Entry
The Cats Entry
```

#### Using jinja expressions
The field specification is a jinja expression for more advanced sorting.
e.g.
```yaml
sort_by:
  - field: quality.resolution
    reverse: yes
  - title|lower
```

## Sorting on multiple fields

Secondary (and further) search fields can be specified by providing the config in a list format.

```yaml
sort_by:
  - field: field1
    reverse: yes
  - field2
```