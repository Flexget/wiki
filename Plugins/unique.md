# Unique

Take action on entries with duplicate fields, except for the first item. `action` defaults to `reject`.

**Syntax:**

```code
unique:
  field: <field name or list of field names>
  action: accept|reject
```

**Example:**

Reject the second+ instance of every movie:

```yaml
tasks:
  mytask:
    rss: https://some.feed/rss.php
    imdb_lookup: yes
    unique:
      field:
        - imdb_id
        - movie_name
      action: reject
```
